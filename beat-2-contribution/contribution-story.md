# Contribution: Updating BrowseModePanel Range of Values for Maximum number of characters on one line Setting

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Wilman Rodriguez
**GitHub Username:** think-tank0
**Issue:** https://github.com/nvaccess/nvda/issues/20478
**Pull Request:** https://github.com/nvaccess/nvda/pull/21105

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: worked on building the issue-scout skill to retrieve and grade GitHub issues based on issue quality and my fit profile.**

I added queries and ranking filters to search-strategy.md. While running the skill, I realized there were a couple of edge cases that needed to be patched. Namely, I updated the issue-is-not-claimed check to also consider comments in the issue body, allowing it to catch cases where the issue author is already working on a fix. I also added a rubric check to discard issues that call out open issues as dependencies.

**Unit 6: worked on updating repro-check skill so that it will work with repos in the wild**

The voice-guard installation steps did not work reliably for Windows, I troubleshooted the issue and realized that Claude did not always use the bash tool when using it on VS Code. I ended up adding a PowerShell specific hook to solve it. The repro-check tool itself did not break.

Did not run into any issues with the memory file.

**Unit 7: worked on installing the ship-gate and manifest to make sure that local branch passed all the needed tests before creating a PR**

I encountered a couple issues when running the ship-gate, first it complained about not having changes against master. I then proceeded to git add all the changed files thinking that was enough, but upon a second failed run, I realized the tool expected the changes to be in a committed stage. After that, the tool ran all the needed tests and reported a pass before running the pr-check skill on `pr_draft.md` which also passed.

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I chose this issue after browsing through all of the Python project issues the course tool returned with a "good first issue" label. The thing that sold me on it was its practicality and narrow scope. I hope to learn more about the project itself, as I've never interacted with similar software in the past. The issue scout tool recommended the issue based on my experience with Python and the fact that the issue scope was well defined by the maintainer. Additionally, it prompted me to confirm that the two previous attempts on the PR were abandoned.

https://github.com/nvaccess/nvda/issues/20478#issuecomment-6479200335

**Toolkit**

- Tool: issue-scout, I used it to process and grade the two issues I short listed after browsing through the course issue browsing tool.
- What it produced: nvaccess/nvda#20478 — accept. Difficulty: straightforward.
- Difficulties: none.
- What changed: Replaced present-technical-details check for more robust scope-feasible check as directed by the assignment. The new check was needed to account for the lack structure and predictability found in live issues, instead of failing issues that are not bounded to a single change, it instead increases their difficulty on the skill report.

---

## Understanding the Issue

**Problem Description**

The Browse Mode "Maximum number of characters on one line" currently has a 10-250 range. The 250 max characters is not enough to read through most paragraphs and should be increased to 1000. Additionally the maintainer suggested a minimum of 0 so that there are no characters limits within the text read while on Browse Mode.

**Expected Behavior**

After the fix, each line read by NVDA should contain up to 1000 characters when the "Maximum number of characters on one line" setting is set to 1000, and should read the entire element content when the setting is set to 0.

**Current Behavior**

The text read by NVDA is limited to have a maximum of 250 characters per line.

**Affected Components**

Min and max values in ```nvda\source\gui\settingsDialogs.py``` for "Maximum number of characters on one line" setting under makeSettings method in the BrowseModePanel class.

**Toolkit**

- Tool: my own understanding of the issue, confirmed by Claude's scoped orientation.
- What it produced: It produced a summary pinpointing where the change needed to solve the issue was and possible places where to add tests for the change.
- Difficulties: the challenge for me was to understand how to reproduce the issue as I was not familiar with Non Visual Desktop Access software, I had to research quite a bit using AI to come up with a way to prove that I was able to reproduce the issue that didn't rely on audio which is one of the main features of NVDA.
- What changed: I initially thought that creating an unit test would suffice to validate the change, but ended up deciding that adding system tests as well would provide a complete coverage for the feature changes.

---

## Reproduction Process

**Environment Setup**
Environment: Python 3.13.15, Windows 11 (x64), Microsoft Edge Version 155.0.4283.45 (Official build) (64-bit), Google Chrome Version 155.0.8059.79 (Official Build) (64-bit), latest master, uv 0.13.6.

Steps: followed steps on contributing.md(projectDocs/dev/contributing.md) for dev environment setup -> create longParagraph.html file with the snippet below -> run source code -> open longParagraph.html on your favorite browser

contributing.md steps
1. Fork repository
2. Clone: git clone --recursive https://github.com/YOUR-USERNAME/nvda.git
3. Keep fork in sync
    ```
    # Add a remote for the NV Access repository.
    git remote add nvaccess https://github.com/nvaccess/nvda.git
    # Fetch the NV Access branches.
    git fetch nvaccess
    # Switch to the local master branch.
    git checkout master
    # Set the local master to use the NV Access master as its upstream.
    git branch -u nvaccess/master
    # Update the local master.
    git pull
    ```
4. Install Microsoft Visual Studio
   
  * Microsoft Visual Studio 2022 or 2026
  * To replicate the production build environment, use the [version of Visual Studio 2022 that GitHub Actions is using](https://github.com/actions/runner-images/tree/main/images/windows).
  * If you don't use the Visual Studio IDE itself, you can download the [build tools](https://aka.ms/vs/17/release/vs_BuildTools.exe).
  * If you do intend to use the Visual Studio IDE (not required for NVDA development), you can download [the community version](https://aka.ms/vs/17/release/vs_Community.exe).
    * The Professional and Enterprise versions are also supported.
    * Preview or insiders versions are *not* supported.
* When installing Visual Studio, additional components must be included:
  * You can automatically fetch these using [NVDAs .vsconfig](../../.vsconfig) using the [import feature of the VS installer](https://learn.microsoft.com/en-us/visualstudio/install/import-export-installation-configurations?view=vs-2022#import-a-configuration).
  * In the list on the Workloads tab, in the Desktop grouping:
    * Desktop development with C++.
      * Once selected, ensure "C++ Clang tools for Windows" is included under the optional grouping.
  * On the Individual components tab, ensure the following items are selected:
    * Windows 11 SDK (10.0.26100.x)
    * MSVC v143 - VS 2022 C++ ARM64/ARM64EC build tools
    * MSVC v143 - VS 2022 C++ x64/x86 build tools
    * C++ ATL for v143 build tools (x86 & x64)
    * C++ ATL for v143 build tools (ARM64/ARM64EC)
5. Build nvda from source: scons source
6. Execute runnvda.bat in the root directory

longParagraph.html
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

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** Speech viewer logs
```
heading    level 1  Long Paragraph Test
word 001 word 002 word 003 word 004 word 005 word 006 word 007 word 008 word 009 word 010 word 011 word 012 word 013 word 014 word 015 word 016 word 017 word 018 word 019 word 020 word 021 word 022 word 023 word 024 word 025 word 026 word 027 word 
028 word 029 word 030 word 031 word 032 word 033 word 034 word 035 word 036 word 037 word 038 word 039 word 040 word 041 word 042 word 043 word 044 word 045 word 046 word 047 word 048 word 049 word 050 word 051 word 052 word 053 word 054 word 055 
word 056 word 057 word 058 word 059 word 060 word 061 word 062 word 063 word 064 word 065 word 066 word 067 word 068 word 069 word 070 word 071 word 072 word 073 word 074 word 075 word 076 word 077 word 078 word 079 word 080 word 081 word 082 word 
083 word 084 word 085 word 086 word 087 word 088 word 089 word 090 word 091 word 092 word 093 word 094 word 095 word 096 word 097 word 098 word 099 word 100 word 101 word 102 word 103 word 104 word 105 word 106 word 107 word 108 word 109 word 110 
word 111 word 112 word 113 word 114 word 115 word 116 word 117 word 118 word 119 word 120 word 121 word 122 word 123 word 124 word 125
```
- **My findings:** I tested the current Behavior of the Browser Mode while reading paragraphs and validated the 250 character limit.

**Toolkit**

- Tool: repro-check, I used the tool to grade the claim comment and repro report draft for the issue.
- What it produced: it accepted both the comment and the repro report.
- Difficulties: setting up the hooks to work on Windows OS.
- What changed: nothing besides the additions to the voice guide.

---

## Solution Approach

**Analysis**

The current 250 "Maximum number of characters on one line" limit is defined in code; the range needs to be updated from 10-250 to 0-1000 as per the maintainer request.

**Proposed Solution**

ln 2616 and 2617 in ```nvda\source\gui\settingsDialogs.py``` need to be updated to the new values so that users can set them up manually via settings.

**Implementation Plan**

1. Update min and max values in ```nvda\source\gui\settingsDialogs.py``` for "Maximum number of characters on one line" setting under makeSettings method in the BrowseModePanel class.
2. Add unit test validating that the BrowseMode setting values can be set as intended.
3. Add system test validating both the 1000 character upper limit behavior and the 0 value unbounded behavior.

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool: plan check, used to grade plan.md and plan-comment.md.
- What it produced: accept.
- Difficulties: The lack of a repro comment proved a challenge for the skill.
- What changed: updated the verdict to pass unclear checks that depended on repro comment.

---

## Testing Strategy

Before

Manual test
```
runnvda.bat
NVDA + Ctrl + B
Set Maximum number of characters on one line to 1000. It will be capped at 250.
NVDA + N -> Tools -> Speech viewer
Open longParagraph.html on browser
Ctrl + Home -> downArrow -> downArrow -> downArrow -> downArrow -> downArrow 
```

Output
```
heading    level 1  Long Paragraph Test
word 001 word 002 word 003 word 004 word 005 word 006 word 007 word 008 word 009 word 010 word 011 word 012 word 013 word 014 word 015 word 016 word 017 word 018 word 019 word 020 word 021 word 022 word 023 word 024 word 025 word 026 word 027 word 
028 word 029 word 030 word 031 word 032 word 033 word 034 word 035 word 036 word 037 word 038 word 039 word 040 word 041 word 042 word 043 word 044 word 045 word 046 word 047 word 048 word 049 word 050 word 051 word 052 word 053 word 054 word 055 
word 056 word 057 word 058 word 059 word 060 word 061 word 062 word 063 word 064 word 065 word 066 word 067 word 068 word 069 word 070 word 071 word 072 word 073 word 074 word 075 word 076 word 077 word 078 word 079 word 080 word 081 word 082 word 
083 word 084 word 085 word 086 word 087 word 088 word 089 word 090 word 091 word 092 word 093 word 094 word 095 word 096 word 097 word 098 word 099 word 100 word 101 word 102 word 103 word 104 word 105 word 106 word 107 word 108 word 109 word 110 
word 111 word 112 word 113 word 114 word 115 word 116 word 117 word 118 word 119 word 120 word 121 word 122 word 123 word 124 word 125
```

After

Manual test
```
runnvda.bat
NVDA + Ctrl + B
Set Maximum number of characters on one line to 1000.
NVDA + N -> Tools -> Speech viewer
Open longParagraph.html on browser
Ctrl + Home -> downArrow -> downArrow
```

Output
```
heading    level 1  Long Paragraph Test
word 001 word 002 word 003 word 004 word 005 word 006 word 007 word 008 word 009 word 010 word 011 word 012 word 013 word 014 word 015 word 016 word 017 word 018 word 019 word 020 word 021 word 022 word 023 word 024 word 025 word 026 word 027 word 028 word 029 word 030 word 031 word 032 word 033 word 034 word 035 word 036 word 037 word 038 word 039 word 040 word 041 word 042 word 043 word 044 word 045 word 046 word 047 word 048 word 049 word 050 word 051 word 052 word 053 word 054 word 055 word 056 word 057 word 058 word 059 word 060 word 061 word 062 word 063 word 064 word 065 word 066 word 067 word 068 word 069 word 070 word 071 word 072 word 073 word 074 word 075 word 076 word 077 word 078 word 079 word 080 word 081 word 082 word 083 word 084 word 085 word 086 word 087 word 088 word 089 word 090 word 091 word 092 word 093 word 094 word 095 word 096 word 097 word 098 word 099 word 100 word 101 word 102 word 103 word 104 word 105 word 106 word 107 word 108 word 109 word 110 word 111 
word 112 word 113 word 114 word 115 word 116 word 117 word 118 word 119 word 120 word 121 word 122 word 123 word 124 word 125
```

Repo tests

Test command: rununittests.bat
```
Running tests...
----------------------------------------------------------------------
sssss.......................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................
----------------------------------------------------------------------
Ran 1516 tests in 21.915s

OK (skipped=5)

Generating XML reports...
```

Lint checker: runlint.bat
```
All checks passed!
810 files left unchanged
WARNING: there is a new pyright version available (v1.1.411 -> v1.1.414).
Please install the new version or set PYRIGHT_PYTHON_FORCE_VERSION to `latest`

0 errors, 0 warnings, 0 informations
All checks passed!
```

Ensure translatable strings have comments for the translators: runcheckpot.bat
```
scons: Reading SConscript files ...
Warning: Building with 1 concurrent job while 20 CPU threads are available. Running SCONS with the parameter '-j20' may lead to a faster build. Running SCONS with parameter '--all-cores' will automatically pick all available cores. 
scons: done reading SConscript files.
scons: Building targets ...
makePot(["output\nvda.pot"], ["source\JABHandler.py", "source\NVDAState.py", "source\RPCConstants.py", "source\XMLFormatting.py", "source\addonAPIVersion.py", "source\annotation.py", "source\api.py", "source\appModuleHandler.py", "source\argsParsing.py", "source\aria.py", "source\audioDucking.py", "source\baseObject.py", "source\bdDetect.py", "source\brailleInput.py", "source\browseMode.py", "source\buildVersion.py", "source\characterProcessing.py", "source\colors.py", "source\comHelper.py", "source\compoundDocuments.py", "source\core.py", "source\cursorManager.py", "source\diffHandler.py", "source\displayModel.py", "source\documentBase.py", "source\documentationUtils.py", "source\driverHandler.py", "source\easeOfAccess.py", "source\editableText.py", "source\eventHandler.py", "source\exceptions.py", "source\fileUtils.py", "source\garbageHandler.py", "source\globalCommands.py", "source\globalPluginHandler.py", "source\globalVars.py", "source\hidpi.py", "source\hwPortUtils.py", "source\inputCore.py", "source\installer.py", "source\jobObject.py", "source\keyCommandsDoc.py", "source\keyLabels.py", "source\keyboardHandler.py", "source\l10nUtil.py", "source\languageHandler.py", "source\localesData.py", "source\locationHelper.py", "source\logHandler.py", "source\louisHelper.py", "source\markdownTranslate.py", "source\mathType.py", "source\md2html.py", "source\mouseHandler.py", "source\msoAutoShapeTypes.py", "source\nvdaBuiltin.py", "source\nvwave.py", "source\objbase.py", "source\objidl.py", "source\oleTypes.py", "source\oleacc.py", "source\pythonConsole.py", "source\queueHandler.py", "source\remotePythonConsole.py", "source\review.py", "source\screenBitmap.py", "source\screenExplorer.py", "source\scriptHandler.py", "source\setup.py", "source\shellapi.py", "source\shlobj.py", "source\speechViewer.py", "source\speechXml.py", "source\synthDriverHandler.py", "source\synthSettingsRing.py", "source\systemUtils.py", "source\tableUtils.py", "source\tones.py", "source\touchHandler.py", "source\touchTracker.py", "source\treeInterceptorHandler.py", "source\ui.py", "source\updateCheck.py", "source\versionInfo.py", "source\vkCodes.py", "source\wasapi.py", "source\watchdog.py", "source\winConsoleHandler.py", "source\winGDI.py", "source\winInputHook.py", "source\winKernel.py", "source\winUser.py", "source\winVersion.py", "source\wincon.py", "source\windowUtils.py", "source\nvda.pyw", "source\nvda_slave.pyw", "source\addonHandler\__init__.py", "source\addonHandler\_pickleToJsonMigration.py", "source\addonHandler\addonVersionCheck.py", "source\addonHandler\packaging.py", "source\addonStore\__init__.py", "source\addonStore\dataManager.py", "source\addonStore\install.py", "source\addonStore\network.py", "source\addonStore\settings.py", "source\addonStore\models\__init__.py", "source\addonStore\models\addon.py", "source\addonStore\models\channel.py", "source\addonStore\models\manifest.py", "source\addonStore\models\scanResults.py", "source\addonStore\models\status.py", "source\addonStore\models\version.py", "source\appModules\1password.py", "source\appModules\__init__.py", "source\appModules\aim.py", "source\appModules\audacity.py", "source\appModules\azardi20.py", "source\appModules\bookshelf.py", "source\appModules\calc.py", "source\appModules\calculator.py", "source\appModules\cicero.py", "source\appModules\code.py", "source\appModules\csrss.py", "source\appModules\devenv.py", "source\appModules\digitaleditions.py", "source\appModules\dllhost.py", "source\appModules\doctts.py", "source\appModules\dosvox.py", "source\appModules\eclipse.py", "source\appModules\egui.py", "source\appModules\esysuite.py", "source\appModules\excel.py", "source\appModules\explorer.py", "source\appModules\fastlogentry.py", "source\appModules\foobar2000.py", "source\appModules\hxmail.py", "source\appModules\instantbird.py", "source\appModules\itunes.py", "source\appModules\javaw.py", "source\appModules\kindle.py", "source\appModules\lockapp.py", "source\appModules\lockapphost.py", "source\appModules\logonui.py", "source\appModules\loudtalks.py", "source\appModules\lync.py", "source\appModules\microsoftedge.py", "source\appModules\microsoftedgecp.py", "source\appModules\mintty.py", "source\appModules\miranda32.py", "source\appModules\mirc.py", "source\appModules\mmc.py", "source\appModules\mplayerc.py", "source\appModules\msedgewebview2.py", "source\appModules\msimn.py", "source\appModules\msnmsgr.py", "source\appModules\nlnotes.py", "source\appModules\notepad.py", "source\appModules\notepadPlusPlus.py", "source\appModules\nvda.py", "source\appModules\obu.py", "source\appModules\openwith.py", "source\appModules\outlook.py", "source\appModules\poedit.py", "source\appModules\powerpnt.py", "source\appModules\putty.py", "source\appModules\searchui.py", "source\appModules\securecrt.py", "source\appModules\shellexperiencehost.py", "source\appModules\skype.py", "source\appModules\soffice.py", "source\appModules\spotify.py", "source\appModules\symphony.py", "source\appModules\systemsettings.py", "source\appModules\taskmgr.py", "source\appModules\teams.py", "source\appModules\teamtalk4classic.py", "source\appModules\thunderbird.py", "source\appModules\totalcmd.py", "source\appModules\ttermpro.py", "source\appModules\tween.py", "source\appModules\utorrent.py", "source\appModules\vipmud.py", "source\appModules\voiceaccess.py", "source\appModules\webconferenceplugin.py", "source\appModules\whatsapp_root.py", "source\appModules\winamp.py", "source\appModules\windowsinternal_composableshell_experiences_textinput_inputapp.py", "source\appModules\winword.py", "source\appModules\wlmail.py", "source\appModules\wwahost.py", "source\appModules\zoom.py", "source\audio\__init__.py", "source\audio\soundSplit.py", "source\autoSettingsUtils\__init__.py", "source\autoSettingsUtils\autoSettings.py", "source\autoSettingsUtils\driverSetting.py", "source\autoSettingsUtils\utils.py", "source\braille\__init__.py", "source\braille\brailleHandler.py", "source\braille\buffers.py", "source\braille\constants.py", "source\braille\extensions.py", "source\braille\formatting.py", "source\braille\labels.py", "source\braille\display\__init__.py", "source\braille\display\driver.py", "source\braille\display\gesture.py", "source\braille\input\__init__.py", "source\braille\input\constants.py", "source\braille\input\gesture.py", "source\braille\input\inputHandler.py", "source\braille\regions\NVDAObject.py", "source\braille\regions\__init__.py", "source\braille\regions\_routing.py", "source\braille\regions\base.py", "source\braille\regions\focus.py", "source\braille\regions\properties.py", "source\braille\regions\textInfo.py", "source\brailleDisplayDrivers\__init__.py", "source\brailleDisplayDrivers\alva.py", "source\brailleDisplayDrivers\baum.py", "source\brailleDisplayDrivers\brailleNote.py", "source\brailleDisplayDrivers\brailliantB.py", "source\brailleDisplayDrivers\brltty.py", "source\brailleDisplayDrivers\ecoBraille.py", "source\brailleDisplayDrivers\freedomScientific.py", "source\brailleDisplayDrivers\handyTech.py", "source\brailleDisplayDrivers\hedoMobilLine.py", "source\brailleDisplayDrivers\hedoProfiLine.py", "source\brailleDisplayDrivers\hidBrailleStandard.py", "source\brailleDisplayDrivers\hims.py", "source\brailleDisplayDrivers\lilli.py", "source\brailleDisplayDrivers\nattiqbraille.py", "source\brailleDisplayDrivers\nlseReaderZoomax.py", "source\brailleDisplayDrivers\noBraille.py", "source\brailleDisplayDrivers\papenmeier.py", "source\brailleDisplayDrivers\papenmeier_serial.py", "source\brailleDisplayDrivers\seika.py", "source\brailleDisplayDrivers\seikantk.py", "source\brailleDisplayDrivers\superBrl.py", "source\brailleDisplayDrivers\albatross\__init__.py", "source\brailleDisplayDrivers\albatross\_threading.py", "source\brailleDisplayDrivers\albatross\constants.py", "source\brailleDisplayDrivers\albatross\driver.py", "source\brailleDisplayDrivers\albatross\gestures.py", "source\brailleDisplayDrivers\dotPad\__init__.py", "source\brailleDisplayDrivers\dotPad\defs.py", "source\brailleDisplayDrivers\dotPad\driver.py", "source\brailleDisplayDrivers\eurobraille\__init__.py", "source\brailleDisplayDrivers\eurobraille\constants.py", "source\brailleDisplayDrivers\eurobraille\driver.py", "source\brailleDisplayDrivers\eurobraille\gestures.py", "source\brailleTables\__init__.py", "source\brailleTables\__tables.py", "source\brailleViewer\__init__.py", "source\brailleViewer\brailleViewerGui.py", "source\brailleViewer\brailleViewerInputGesture.py", "source\COMRegistrationFixes\__init__.py", "source\config\__init__.py", "source\config\aggregatedSection.py", "source\config\configDefaults.py", "source\config\configFlags.py", "source\config\configSections.py", "source\config\configSpec.py", "source\config\featureFlag.py", "source\config\featureFlagEnums.py", "source\config\profileUpgradeSteps.py", "source\config\profileUpgrader.py", "source\config\registry.py", "source\contentRecog\__init__.py", "source\contentRecog\_wgcCapture.py", "source\contentRecog\recogUi.py", "source\contentRecog\uwpOcr.py", "source\controlTypes\__init__.py", "source\controlTypes\deprecatedAliases.py", "source\controlTypes\descriptionFrom.py", "source\controlTypes\formatFields.py", "source\controlTypes\isCurrent.py", "source\controlTypes\outputReason.py", "source\controlTypes\processAndLabelStates.py", "source\controlTypes\role.py", "source\controlTypes\roleAndStateSpecialCases.py", "source\controlTypes\state.py", "source\documentNavigation\paragraphHelper.py", "source\documentNavigation\sentenceHelper.py", "source\extensionPoints\__init__.py", "source\extensionPoints\util.py", "source\fonts\__init__.py", "source\ftdi2\__init__.py", "source\ftdi2\ftd2xx.py", "source\globalPlugins\__init__.py", "source\gui\_SetURLDialog.py", "source\gui\__init__.py", "source\gui\addonGui.py", "source\gui\blockAction.py", "source\gui\configManagement.py", "source\gui\configProfiles.py", "source\gui\contextHelp.py", "source\gui\dpiScalingHelper.py", "source\gui\exit.py", "source\gui\guiHelper.py", "source\gui\inputGestures.py", "source\gui\installerGui.py", "source\gui\logViewer.py", "source\gui\message.py", "source\gui\nvdaControls.py", "source\gui\persistenceHandler.py", "source\gui\settingsDialogs.py", "source\gui\speechDict.py", "source\gui\startupDialogs.py", "source\gui\addonStoreGui\__init__.py", "source\gui\addonStoreGui\controls\__init__.py", "source\gui\addonStoreGui\controls\actions.py", "source\gui\addonStoreGui\controls\addonList.py", "source\gui\addonStoreGui\controls\details.py", "source\gui\addonStoreGui\controls\messageDialogs.py", "source\gui\addonStoreGui\controls\storeDialog.py", "source\gui\addonStoreGui\viewModels\__init__.py", "source\gui\addonStoreGui\viewModels\action.py", "source\gui\addonStoreGui\viewModels\addonList.py", "source\gui\addonStoreGui\viewModels\store.py", "source\hwIo\__init__.py", "source\hwIo\base.py", "source\hwIo\hid.py", "source\hwIo\ioThread.py", "source\hwIo\ble\__init__.py", "source\hwIo\ble\_io.py", "source\hwIo\ble\_scanner.py", "source\IAccessibleHandler\__init__.py", "source\IAccessibleHandler\internalWinEventHandler.py", "source\IAccessibleHandler\orderedWinEventLimiter.py", "source\IAccessibleHandler\types.py", "source\IAccessibleHandler\utils.py", "source\louis\__init__.py", "source\mathPres\__init__.py", "source\mathPres\_mathMlNode.py", "source\mathPres\MathCAT\MathCAT.py", "source\mathPres\MathCAT\__init__.py", "source\mathPres\MathCAT\_navNodeMapping.py", "source\mathPres\MathCAT\localization.py", "source\mathPres\MathCAT\navCommands.py", "source\mathPres\MathCAT\preferences.py", "source\mathPres\MathCAT\rulesUtils.py", "source\mathPres\MathCAT\speech.py", "source\monkeyPatches\__init__.py", "source\monkeyPatches\comtypesMonkeyPatches.py", "source\monkeyPatches\wxMonkeyPatches.py", "source\NVDAHelper\__init__.py", "source\NVDAHelper\localLib.py", "source\NVDAHelper\localWin10.py", "source\NVDAObjects\__init__.py", "source\NVDAObjects\behaviors.py", "source\NVDAObjects\inputComposition.py", "source\NVDAObjects\lockscreen.py", "source\NVDAObjects\IAccessible\MSHTML.py", "source\NVDAObjects\IAccessible\SysMonthCal32.py", "source\NVDAObjects\IAccessible\__init__.py", "source\NVDAObjects\IAccessible\adobeAcrobat.py", "source\NVDAObjects\IAccessible\akelEdit.py", "source\NVDAObjects\IAccessible\chromium.py", "source\NVDAObjects\IAccessible\delphi.py", "source\NVDAObjects\IAccessible\hh.py", "source\NVDAObjects\IAccessible\ia2TextMozilla.py", "source\NVDAObjects\IAccessible\ia2Web.py", "source\NVDAObjects\IAccessible\mozilla.py", "source\NVDAObjects\IAccessible\msOffice.py", "source\NVDAObjects\IAccessible\mscandui.py", "source\NVDAObjects\IAccessible\qt.py", "source\NVDAObjects\IAccessible\scintilla.py", "source\NVDAObjects\IAccessible\sysListView32.py", "source\NVDAObjects\IAccessible\sysTreeView32.py", "source\NVDAObjects\IAccessible\webKit.py", "source\NVDAObjects\IAccessible\winConsole.py", "source\NVDAObjects\IAccessible\winword.py", "source\NVDAObjects\IAccessible\wx.py", "source\NVDAObjects\JAB\__init__.py", "source\NVDAObjects\UIA\VisualStudio.py", "source\NVDAObjects\UIA\__init__.py", "source\NVDAObjects\UIA\anaheimEdge.py", "source\NVDAObjects\UIA\chromium.py", "source\NVDAObjects\UIA\excel.py", "source\NVDAObjects\UIA\spartanEdge.py", "source\NVDAObjects\UIA\sysListView32.py", "source\NVDAObjects\UIA\web.py", "source\NVDAObjects\UIA\winConsoleUIA.py", "source\NVDAObjects\UIA\wordDocument.py", "source\NVDAObjects\window\__init__.py", "source\NVDAObjects\window\_msOffice.py", "source\NVDAObjects\window\_msOfficeChart.py", "source\NVDAObjects\window\akelEdit.py", "source\NVDAObjects\window\edit.py", "source\NVDAObjects\window\excel.py", "source\NVDAObjects\window\excelCellBorder.py", "source\NVDAObjects\window\scintilla.py", "source\NVDAObjects\window\winConsole.py", "source\NVDAObjects\window\winword.py", "source\screenCurtain\__init__.py", "source\screenCurtain\_screenCurtain.py", "source\speech\__init__.py", "source\speech\commands.py", "source\speech\extensions.py", "source\speech\languageHandling.py", "source\speech\manager.py", "source\speech\priorities.py", "source\speech\sayAll.py", "source\speech\shortcutKeys.py", "source\speech\speech.py", "source\speech\speechWithoutPauses.py", "source\speech\types.py", "source\speechDictHandler\__init__.py", "source\speechDictHandler\definitions.py", "source\speechDictHandler\dictFormatUpgrade.py", "source\speechDictHandler\types.py", "source\synthDrivers\__init__.py", "source\synthDrivers\_espeak.py", "source\synthDrivers\_sonic.py", "source\synthDrivers\espeak.py", "source\synthDrivers\mssp.py", "source\synthDrivers\oneCore.py", "source\synthDrivers\sapi4_32.py", "source\synthDrivers\sapi5.py", "source\synthDrivers\sapi5_32.py", "source\synthDrivers\silence.py", "source\tactile\__init__.py", "source\tactile\braille.py", "source\textInfos\__init__.py", "source\textInfos\offsets.py", "source\textUtils\__init__.py", "source\textUtils\_braille.py", "source\textUtils\hyphenation.py", "source\textUtils\icu.py", "source\textUtils\segFlag.py", "source\textUtils\uniscribe.py", "source\textUtils\_wordSeg\__init__.py", "source\textUtils\_wordSeg\wordSegStrategy.py", "source\textUtils\_wordSeg\wordSegUtils.py", "source\textUtils\_wordSeg\wordSegmenter.py", "source\UIAHandler\__init__.py", "source\UIAHandler\browseMode.py", "source\UIAHandler\constants.py", "source\UIAHandler\customAnnotations.py", "source\UIAHandler\customProps.py", "source\UIAHandler\remote.py", "source\UIAHandler\types.py", "source\UIAHandler\utils.py", "source\UIAHandler\_remoteOps\__init__.py", "source\UIAHandler\_remoteOps\builder.py", "source\UIAHandler\_remoteOps\localExecute.py", "source\UIAHandler\_remoteOps\lowLevel.py", "source\UIAHandler\_remoteOps\operation.py", "source\UIAHandler\_remoteOps\remoteAPI.py", "source\UIAHandler\_remoteOps\remoteAlgorithms.py", "source\UIAHandler\_remoteOps\remoteFuncWrapper.py", "source\UIAHandler\_remoteOps\instructions\__init__.py", "source\UIAHandler\_remoteOps\instructions\_base.py", "source\UIAHandler\_remoteOps\instructions\arithmetic.py", "source\UIAHandler\_remoteOps\instructions\array.py", "source\UIAHandler\_remoteOps\instructions\bool.py", "source\UIAHandler\_remoteOps\instructions\cacheRequest.py", "source\UIAHandler\_remoteOps\instructions\controlFlow.py", "source\UIAHandler\_remoteOps\instructions\element.py", "source\UIAHandler\_remoteOps\instructions\extension.py", "source\UIAHandler\_remoteOps\instructions\float.py", "source\UIAHandler\_remoteOps\instructions\general.py", "source\UIAHandler\_remoteOps\instructions\guid.py", "source\UIAHandler\_remoteOps\instructions\int.py", "source\UIAHandler\_remoteOps\instructions\null.py", "source\UIAHandler\_remoteOps\instructions\status.py", "source\UIAHandler\_remoteOps\instructions\string.py", "source\UIAHandler\_remoteOps\instructions\textRange.py", "source\UIAHandler\_remoteOps\remoteTypes\__init__.py", "source\UIAHandler\_remoteOps\remoteTypes\cacheRequest.py", "source\UIAHandler\_remoteOps\remoteTypes\element.py", "source\UIAHandler\_remoteOps\remoteTypes\extensionTarget.py", "source\UIAHandler\_remoteOps\remoteTypes\intEnum.py", "source\UIAHandler\_remoteOps\remoteTypes\textRange.py", "source\utils\__init__.py", "source\utils\_crashHandler.py", "source\utils\_deprecate.py", "source\utils\blockUntilConditionMet.py", "source\utils\caseInsensitiveCollections.py", "source\utils\debounce.py", "source\utils\displayString.py", "source\utils\localisation.py", "source\utils\mmdevice.py", "source\utils\raii.py", "source\utils\schedule.py", "source\utils\security.py", "source\utils\tempFile.py", "source\utils\urlUtils.py", "source\virtualBuffers\MSHTML.py", "source\virtualBuffers\__init__.py", "source\virtualBuffers\adobeAcrobat.py", "source\virtualBuffers\gecko_ia2.py", "source\virtualBuffers\lotusNotes.py", "source\virtualBuffers\webKit.py", "source\vision\__init__.py", "source\vision\constants.py", "source\vision\exceptions.py", "source\vision\providerBase.py", "source\vision\providerInfo.py", "source\vision\util.py", "source\vision\visionHandler.py", "source\vision\visionHandlerExtensionPoints.py", "source\visionEnhancementProviders\NVDAHighlighter.py", "source\visionEnhancementProviders\__init__.py", "source\visionEnhancementProviders\_exampleProvider_autoGui.py", "source\winAPI\__init__.py", "source\winAPI\_displayTracking.py", "source\winAPI\_powerTracking.py", "source\winAPI\_wtsApi32.py", "source\winAPI\constants.py", "source\winAPI\dpiAwareness.py", "source\winAPI\messageWindow.py", "source\winAPI\secureDesktop.py", "source\winAPI\sessionTracking.py", "source\winAPI\types.py", "source\winAPI\winUser\__init__.py", "source\winAPI\winUser\constants.py", "source\winAPI\winUser\functions.py", "source\winBindings\__init__.py", "source\winBindings\advapi32.py", "source\winBindings\bthprops.py", "source\winBindings\cfgmgr32.py", "source\winBindings\commCtrl.py", "source\winBindings\crypt32.py", "source\winBindings\dbgHelp.py", "source\winBindings\gdi32.py", "source\winBindings\gdiplus.py", "source\winBindings\hid.py", "source\winBindings\icu.py", "source\winBindings\jobapi2.py", "source\winBindings\kernel32.py", "source\winBindings\magnification.py", "source\winBindings\mmeapi.py", "source\winBindings\mshtml.py", "source\winBindings\ole32.py", "source\winBindings\oleacc.py", "source\winBindings\oleaut32.py", "source\winBindings\rpcrt4.py", "source\winBindings\sas.py", "source\winBindings\setupapi.py", "source\winBindings\shcore.py", "source\winBindings\shell32.py", "source\winBindings\shlwapi.py", "source\winBindings\uiAutomationCore.py", "source\winBindings\urlmon.py", "source\winBindings\user32.py", "source\winBindings\version.py", "source\winBindings\winmm.py", "source\winBindings\winusb.py", "source\winBindings\wtsapi32.py", "source\_asyncioEventLoop\__init__.py", "source\_asyncioEventLoop\_state.py", "source\_asyncioEventLoop\utils.py", "source\_bridge\__init__.py", "source\_bridge\base.py", "source\_bridge\clients\synthDriverHost32\launcher.py", "source\_bridge\clients\synthDriverHost32\synthDriver.py", "source\_bridge\components\proxies\nvwave.py", "source\_bridge\components\proxies\synthDriver.py", "source\_bridge\components\services\__init__.py", "source\_bridge\components\services\nvwave.py", "source\_bridge\components\services\synthDriver.py", "source\_bridge\runtimes\synthDriverHost\audioDucking.py", "source\_bridge\runtimes\synthDriverHost\config.py", "source\_bridge\runtimes\synthDriverHost\core.py", "source\_bridge\runtimes\synthDriverHost\globalVars.py", "source\_bridge\runtimes\synthDriverHost\logHandler.py", "source\_bridge\runtimes\synthDriverHost\speechDictHandler.py", "source\_bridge\runtimes\synthDriverHost\synthDriverHost.py", "source\_bridge\runtimes\synthDriverHost\synthSettingsRing.py", "source\_bridge\runtimes\synthDriverHost\main.pyw", "source\_bridge\runtimes\synthDriverHost\speech\__init__.py", "source\_bridge\runtimes\synthDriverHost\speech\commands.py", "source\_bridge\runtimes\synthDriverHost\speech\types.py", "source\_bridge\runtimes\synthDriverHost\synthDrivers\__init__.py", "source\_magnifier\__init__.py", "source\_magnifier\commands.py", "source\_magnifier\config.py", "source\_magnifier\dockedMagnifier.py", "source\_magnifier\fixedMagnifier.py", "source\_magnifier\fullscreenMagnifier.py", "source\_magnifier\lensMagnifier.py", "source\_magnifier\magnifier.py", "source\_magnifier\utils\__init__.py", "source\_magnifier\utils\errorHandling.py", "source\_magnifier\utils\filterHandler.py", "source\_magnifier\utils\focusManager.py", "source\_magnifier\utils\mouseHook.py", "source\_magnifier\utils\spotlightManager.py", "source\_magnifier\utils\types.py", "source\_remoteClient\__init__.py", "source\_remoteClient\bridge.py", "source\_remoteClient\client.py", "source\_remoteClient\configuration.py", "source\_remoteClient\connectionInfo.py", "source\_remoteClient\cues.py", "source\_remoteClient\dialogs.py", "source\_remoteClient\input.py", "source\_remoteClient\localMachine.py", "source\_remoteClient\menu.py", "source\_remoteClient\protocol.py", "source\_remoteClient\secureDesktop.py", "source\_remoteClient\serializer.py", "source\_remoteClient\server.py", "source\_remoteClient\session.py", "source\_remoteClient\transport.py", "source\_remoteClient\urlHandler.py", "source\_synthDrivers32\__init__.py", "source\_synthDrivers32\_sapi4.py", "source\_synthDrivers32\_sapi5.py", "source\_synthDrivers32\_sonic.py", "source\_synthDrivers32\sapi4.py", "source\_synthDrivers32\sapi5.py"])
cd source && C:\Coding\nvda\miscDeps\tools\xgettext.exe -o C:\Coding\nvda\output\nvda.pot --package-name NVDA --package-version source-20478-updating-max-number-of-characters-in-line-8475635 --foreign-user --add-comments=Translators: --keyword=pgettext:1c,2 --keyword=npgettext:1c,2,3 --from-code utf-8 --language=python --files-from=C:\Coding\nvda\output\potSourceFileList.txt
scons: done building targets.
0 errors, 0 unexpected successes, 55 expected errors, 0 messages marked as expected errors not present in the source code
```

Check that you don't introduce any new python dependencies with incompatible licenses: runlicensecheck.bat
```
2026-11-02 16:43:12.949 | WARNING  | licensecheck.license_matrix:_licenseLookup:130 - 'ZLIB' License not identified so falling back to UNKNOWN
                                                      
                         Info                         
┏━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Item            ┃ Value                            ┃
┡━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ program         │ licensecheck                     │
│ version         │ 2026.0.8                         │
│ license         │ MIT LICENSE                      │
│ project_license │ GPL-2.0-OR-LATER/ GPLV2+ LICENSE │
└─────────────────┴──────────────────────────────────┘
                                                                                                    
                                          List Of Packages                                          
┏━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Compatible ┃ Package                                  ┃ License(s)                               ┃
┡━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ ✔          │ attrs                                    │ MIT                                      │
│ ✔          │ bleak                                    │ MIT                                      │
│ ✔          │ certifi                                  │ Mozilla Public License 2.0 _MPL 2.0_     │
│ ✔          │ cffi                                     │ MIT-0                                    │
│ ✔          │ charset-normalizer                       │ MIT                                      │
│ ✔          │ comtypes                                 │ MIT                                      │
│ ✔          │ configobj                                │ BSD License                              │
│ ✔          │ crowdin-api-client                       │ MIT                                      │
│ ✔          │ cryptography                             │ Apache-2.0;; BSD-3-Clause                │
│ ✔          │ deprecated                               │ MIT                                      │
│ ✔          │ detect-secrets                           │ Apache Software License                  │
│ ✔          │ fast-diff-match-patch                    │ Apache License 2.0                       │
│ ✔          │ fuzzysearch                              │ MIT License                              │
│ ✔          │ idna                                     │ BSD-3-Clause                             │
│ ✔          │ l2m4m                                    │ GNU General Public License v3 _GPLv3_    │
│ ✔          │ latex2mathml                             │ MIT                                      │
│ ✔          │ lxml                                     │ BSD-3-Clause                             │
│ ✔          │ markdown                                 │ BSD-3-Clause                             │
│ ✔          │ markdown-link-attr-modifier              │ GNU General Public License v3 _GPLv3_    │
│ ✔          │ mdx-gh-links                             │ BSD License                              │
│ ✔          │ mdx-truly-sane-lists                     │ MIT License                              │
│ ✔          │ nh3                                      │ MIT                                      │
│ ✔          │ numpy                                    │ 0BSD;; BSD-3-Clause;; CC0-1.0;; MIT;;    │
│            │                                          │ Zlib                                     │
│ ✔          │ plumbum                                  │ MIT                                      │
│ ✔          │ psutil                                   │ BSD-3-Clause                             │
│ ✔          │ pycaw                                    │ MIT                                      │
│ ✔          │ pycparser                                │ BSD-3-Clause                             │
│ ✔          │ pymdown-extensions                       │ MIT                                      │
│ ✔          │ pyphen                                   │ GNU General Public License v2;; GNU      │
│            │                                          │ Lesser General Public License v2;;       │
│            │                                          │ Mozilla Public License 1.1 _MPL 1.1_;;   │
│            │                                          │ later _GPLv2__;; later _LGPLv2__         │
│ ✔          │ pyserial                                 │ BSD License                              │
│ ✔          │ pywin32                                  │ Python Software Foundation License       │
│ ✔          │ pyyaml                                   │ MIT License                              │
│ ✔          │ regex                                    │ Apache-2.0;; CNRI-Python                 │
│ ✔          │ requests                                 │ Apache Software License                  │
│ ✔          │ rpyc                                     │ MIT License                              │
│ ✔          │ schedule                                 │ MIT License                              │
│ ✔          │ typing-extensions                        │ PSF-2.0                                  │
│ ✔          │ url-normalize                            │ MIT                                      │
│ ✔          │ urllib3                                  │ MIT                                      │
│ ✔          │ winrt-runtime                            │ MIT                                      │
│ ✔          │ winrt-windows-devices-bluetooth          │ MIT                                      │
│ ✔          │ winrt-windows-devices-bluetooth-adverti… │ MIT                                      │
│ ✔          │ winrt-windows-devices-bluetooth-generic… │ MIT                                      │
│ ✔          │ winrt-windows-devices-enumeration        │ MIT                                      │
│ ✔          │ winrt-windows-devices-radios             │ MIT                                      │
│ ✔          │ winrt-windows-foundation                 │ MIT                                      │
│ ✔          │ winrt-windows-foundation-collections     │ MIT                                      │
│ ✔          │ winrt-windows-storage-streams            │ MIT                                      │
│ ✔          │ wrapt                                    │ BSD-2-Clause                             │
│ ✔          │ wxpython                                 │ LGPL-2.0-or-later WITH                   │
│            │                                          │ WxWindows-exception-3.1                  │
└────────────┴──────────────────────────────────────────┴──────────────────────────────────────────┘
```

**Toolkit**

- Tool: pr-precheck. I used it to make sure that my plan.md, pr_draft.md, and test_evidence.md were coherent and addressed the requirements in the PR template.
- What it produced: accept.
- Difficulties: I realized I had some inconsistencies in between some of the files and was able to address them with the tool feedback.
- What changed: Nothing. I just had to add the title to the top of the PR draft momentarily.

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** https://github.com/nvaccess/nvda/pull/21105

**PR Description:** When browse mode is set to use screen layout navigation, paragraphs exceeding 250 characters are frequently encountered and are often split at awkward places. Increasing the limit to 1000 and adding 0 as an option will help to improve user experience.

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]
- None yet.

**Status:** Awaiting review

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
