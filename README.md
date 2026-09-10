# Contribution 1: DrumBeatRepo

**Contribution Number:** 1 

**Student:** Dominique Fraser 

**Issue:** https://github.com/Babali42/DrumBeatRepo/issues/511  

**Status:** Phase 1 -- Complete

---

## Why I Chose This Issue

I chose Issue #511 because it was the open-source project and issue that interested me the most out of the three options we reviewed. I was drawn to DrumBeatRepo because it combines software development with music, which makes the project more engaging to me than working on a completely unfamiliar type of application. The issue itself is also approachable because it involves adding a missing SVG icon for the crash cymbal in the Rock Variation Pattern rather than making a large or complicated change to the application. I liked that I could understand the goal of the issue while still being introduced to how a real open-source project organizes its UI assets, code, and tests.

This issue also matches my background in computer science and my interest in gaining more practical software development experience. While I have experience with programming and different areas of technology, I want to become more comfortable understanding an existing codebase and contributing to a project that I did not create myself. Through this issue, I hope to learn more about how developers investigate bugs, identify the files that need to be changed, use GitHub and Git for collaboration, test their changes, and ultimately contribute to an open-source project. I also think starting with a smaller UI-focused issue will give me a good foundation for tackling more complex open-source contributions in the future.

---

## Understanding the Issue

### Problem Description

The Rock Variation Pattern in DrumBeatRepo is missing a visual icon for the crash cymbal. The crash cymbal is already configured to use MIDI note 49, so the functionality is recognized by the application, but there is no corresponding SVG drum icon being displayed for it. The issue is therefore primarily a UI/visual asset problem rather than a problem with the drum pattern or MIDI configuration.

### Expected Behavior

When the Rock Variation Pattern includes a crash cymbal, the application should display a crash cymbal icon along with the other drum instrument icons. The crash cymbal should have its own SVG image that is correctly mapped to the instrument so that users can visually identify it in the interface.

### Current Behavior

The application recognizes the crash cymbal through MIDI note 49, but there is no crash cymbal SVG icon available for the UI to display. As a result, the crash cymbal does not have the appropriate visual representation when viewing the Rock Variation Pattern.

### Affected Components

The main components involved are the Rock Variation Pattern data in src/assets/beats/rock/variation.json and the drum image pipe and its tests in src/app/ui/pipes/drum-image.pipe.spec.ts. The issue also involves adding the appropriate SVG asset for the crash cymbal and making sure the UI correctly maps the instrument to that image.

---

## Reproduction Process

### Environment Setup

The professor handled the local development environment setup during the class walkthrough, so I did not personally install or configure the project. The project consists of a Scala engine and an Angular frontend. The engine is built using sbt, while the frontend uses Node.js and npm. The professor followed the project’s setup process to get the application running locally.

### Steps to Reproduce

1. Open the DrumBeatRepo application and navigate to the Rock Variation Pattern.
2. Examine the drum instruments displayed in the pattern, specifically the crash cymbal.
3. Observe the visual representation associated with the crash cymbal.

### Observed Result

The crash cymbal is recognized by the application through its configured MIDI note, but it does not have a corresponding visual icon in the interface. The other drum instruments have visual representations, while the crash cymbal is missing its SVG icon.

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/shanker-codepath/DrumBeatRepo/tree/cymbal-image
- **Screenshots/logs:** N/A
- **My findings:** The reproduction confirmed that the issue is primarily a missing UI asset rather than a problem with the crash cymbal’s MIDI configuration. The crash cymbal is already associated with MIDI note 49, but the application is missing the SVG image needed to visually represent it. This helped me understand that the fix will likely involve the drum image mapping and the appropriate SVG asset rather than changing the underlying drum pattern or audio functionality.

---

## Solution Approach

### Analysis

The crash cymbal uses MIDI note 49, but MIDI note 49 isn’t included in the drumImages mapping in DrumImagePipe. Because unmapped MIDI values fall back to default.svg, the crash cymbal displays the default image.

### Proposed Solution

Files I Expect to Touch

* frontend/src/app/ui/pipes/drum-image.pipe.ts — Add the MIDI 49 to crash cymbal image mapping.
* frontend/src/app/ui/pipes/drum-image.pipe.spec.ts — Update the crash cymbal test to expect the new image.
* frontend/src/assets/images/drums/ — Add the new crash cymbal SVG asset.

I do not expect to modify frontend/src/assets/beats/rock/variation.json because the crash cymbal and MIDI note 49 are already correctly configured there.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** The Rock Variation Pattern includes a crash cymbal with MIDI note 49, but the application does not display a crash cymbal icon for it. The crash cymbal’s audio and MIDI configuration already exist in variation.json, so the problem is with how the UI maps MIDI drum types to their corresponding SVG images.

Currently, the DrumImagePipe contains mappings for the kick, snare, and hi-hat MIDI notes, but it does not contain a mapping for MIDI note 49. When the pipe receives an unmapped MIDI value, it falls back to default.svg. The existing unit test confirms this behavior because the crash cymbal currently expects the default image.

**Match:** The existing DrumImagePipe provides the pattern for solving the issue. It uses the drumImages object to associate MIDI note numbers with SVG image names. For example, MIDI note 36 maps to kick, MIDI note 38 maps to snare, and MIDI notes 42 and 46 map to hihats.

The crash cymbal can follow the same pattern by adding MIDI note 49 to this mapping and assigning it to a crash cymbal SVG image. The existing crash cymbal test in drum-image.pipe.spec.ts can then be updated to expect the new crash cymbal image instead of the default image.

**Plan:** 
1. Add a crash cymbal SVG asset to the application’s drum image assets.
2. Update drum-image.pipe.ts so MIDI note 49 maps to the new crash cymbal image.
3. Update the existing crash cymbal test in drum-image.pipe.spec.ts so it expects the crash cymbal SVG instead of default.svg.
4. Run the relevant frontend unit tests to verify that the new mapping works.
5. Run the project’s frontend test suite to make sure the change does not break the existing drum image mappings or other functionality.
6. Manually verify the Rock Variation Pattern displays the crash cymbal icon correctly.

**Implement:** https://github.com/shanker-codepath/DrumBeatRepo/tree/cymbal-image

**Review:** Before submitting the change, I will review the project’s contribution guidelines and make sure my branch follows the repository’s workflow. The project’s README recommends forking the repository, creating a branch from main, making the changes, passing the tests, and opening a pull request. (GitHub⁠￼)

I will also review the final diff to make sure only the files necessary for the issue were changed, the SVG asset is appropriate, the test accurately represents the expected behavior, and there are no unrelated changes.

**Evaluate:** I will first run the existing DrumImagePipe tests and confirm that the crash cymbal test now passes with the new SVG path. I will also run the frontend test suite using the project’s documented test command to make sure the existing kick, snare, hi-hat, and default-image behavior still works. The repository documents npm run test for the Angular/Karma tests and npm run test-vitest for the Vitest tests. (GitHub⁠￼)

Finally, I will manually check the Rock Variation Pattern in the application to confirm that the crash cymbal now displays its own icon rather than the default drum image.

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
