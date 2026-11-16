# Improved Browsing Experience for Screen Reader Software Users

## Overview

This fall, I worked on creating different AI skills that aided me in contributing to an open source project. The skills mostly acted as guidelines when it came to the process of selecting an issue, creating evidence based issue reproduction, planning a fix, and finally publishing a PR. The feature itself was a simple range change for a Browse specific setting controlling how many characters the tool read at a time when parsing browser text. It initially read 10 to 250 characters at a time, which made synthetic speech/refreshable braille stop at awkward places when the converted text section was too large. The maintainers requested that the range be moved to 0-1000, which would make for a better user experience. The PR (https://github.com/nvaccess/nvda/pull/21105) got one approval after removing unit tests as per maintainer request and is awaiting another review.

## What happened

After browsing through hundreds of open source project issues, I found https://github.com/nvaccess/nvda/issues/20478, which seemed like a feature that would improve the day to day experience of the tool's users. After observing a couple of abandoned PRs, I deemed there was still work to be done on the PR that would be a nice learning experience for me, given that I hadn't worked with screen reader software in the past. The requested change was simple to implement, as it was just a change to a couple of hardcoded values (see diff below).

```diff
 class BrowseModePanel(SettingsPanel):
 	# Translators: This is the label for the browse mode settings panel.
 	title = _("Browse Mode")
 	helpId = "BrowseModeSettings"

 	def makeSettings(self, settingsSizer):
 		sHelper = guiHelper.BoxSizerHelper(self, sizer=settingsSizer)
 		# Translators: This is the label for a textfield in the
 		# browse mode settings panel.
 		maxLengthLabelText = _("&Maximum number of characters on one line")
 		self.maxLengthEdit = sHelper.addLabeledControl(
 			maxLengthLabelText,
 			nvdaControls.SelectOnFocusSpinCtrl,
 			# min and max are not enforced in the config for virtualBuffers.maxLineLength
-			min=10,
-			max=250,
+			min=0,
+			max=1000,
 			initial=config.conf["virtualBuffers"]["maxLineLength"],
 		)
 		self.bindHelpEvent("BrowseModeSettingsMaxLength", self.maxLengthEdit)
```

The hardest challenge for me was understanding the user experience being described in the issue as someone who primarily relies on their eyes while testing software aimed at people who cannot rely alone on what they see alone. This required me to read the NVDA documentation and to learn through experience, and AI prompting, the purpose of BrowseMode and how to interact with a website via keyboard to create a manual test that would help others understand the need for the feature and validate the change in behavior after merging the PR changes. This is the test I came up with:

Create longParagraph.html locally
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Long Paragraph Test</title>
</head>
<body>

<h1>Long Paragraph Test</h1>

<p id="target">
word 001 word 002 word 003 word 004 word 005 word 006 word 007 word 008 word 009 word 010 word 011 word 012 word 013 word 014 word 015 word 016 word 017 word 018 word 019 word 020 word 021 word 022 word 023 word 024 word 025 word 026 word 027 word 028 word 029 word 030 word 031 word 032 word 033 word 034 word 035 word 036 word 037 word 038 word 039 word 040 word 041 word 042 word 043 word 044 word 045 word 046 word 047 word 048 word 049 word 050 word 051 word 052 word 053 word 054 word 055 word 056 word 057 word 058 word 059 word 060 word 061 word 062 word 063 word 064 word 065 word 066 word 067 word 068 word 069 word 070 word 071 word 072 word 073 word 074 word 075 word 076 word 077 word 078 word 079 word 080 word 081 word 082 word 083 word 084 word 085 word 086 word 087 word 088 word 089 word 090 word 091 word 092 word 093 word 094 word 095 word 096 word 097 word 098 word 099 word 100 word 101 word 102 word 103 word 104 word 105 word 106 word 107 word 108 word 109 word 110 word 111 word 112 word 113 word 114 word 115 word 116 word 117 word 118 word 119 word 120 word 121 word 122 word 123 word 124 word 125
</p>

</body>
</html>
```
**Steps to Reproduce**

Manual test
```
runnvda.bat
NVDA + Ctrl + B
Set Maximum number of characters on one line to 1000. It will be capped at 250.
NVDA + N -> Tools -> Speech viewer
Open longParagraph.html on browser
Ctrl + Home -> downArrow -> downArrow -> downArrow -> downArrow -> downArrow 
```

You should hear the following sentences after following the steps above. (Copied from Speech Viewer output)

```
heading    level 1  Long Paragraph Test

word 001 word 002 word 003 word 004 word 005 word 006 word 007 word 008 word 009 word 010 word 011 word 012 word 013 word 014 word 015 word 016 word 017 word 018 word 019 word 020 word 021 word 022 word 023 word 024 word 025 word 026 word 027 word 

028 word 029 word 030 word 031 word 032 word 033 word 034 word 035 word 036 word 037 word 038 word 039 word 040 word 041 word 042 word 043 word 044 word 045 word 046 word 047 word 048 word 049 word 050 word 051 word 052 word 053 word 054 word 055 

word 056 word 057 word 058 word 059 word 060 word 061 word 062 word 063 word 064 word 065 word 066 word 067 word 068 word 069 word 070 word 071 word 072 word 073 word 074 word 075 word 076 word 077 word 078 word 079 word 080 word 081 word 082 word 

083 word 084 word 085 word 086 word 087 word 088 word 089 word 090 word 091 word 092 word 093 word 094 word 095 word 096 word 097 word 098 word 099 word 100 word 101 word 102 word 103 word 104 word 105 word 106 word 107 word 108 word 109 word 110 

word 111 word 112 word 113 word 114 word 115 word 116 word 117 word 118 word 119 word 120 word 121 word 122 word 123 word 124 word 125
```

After understanding how to test the behavior, it was easier to ask Claude to create a system test replicating the manual test. Little did Claude and I know that we'd run into a quirk of the testing speech-to-text test functionality available for the Robot Framework setup. Essentially, the first iteration used a function to create a 1000 word space separated string with the format "word001 word002 ...". The issue was that the speech-to-text function would introduce a space "word 001", making it so that the text representation of the spoken text didn't match the original. At this point, Claude came up with an overly convoluted version of the test using characters instead of numbers "wordaaa wordaab ...", which also introduced other requirements into the text file. I ended up backtracking the changes and directing Claude on how to proceed with a simpler approach by adding spaces to the original word format "word 001", which allowed the two tests to pass. Currently, the PR has been acknowledged by a maintainer, approved by another, and is finally waiting for another review before merging.

## Limitations and what's next
A current limitation is that the behavior of the getSpeechAfterKey method alters the original text. Fixing this would require finding the root of the issue separating text like "word001" into "word 001" so that, in the future, contributors do not have to change tests to accommodate testing method behavior that does not reflect real world NVDA behavior. 
