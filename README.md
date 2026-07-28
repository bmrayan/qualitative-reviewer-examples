# Qualitative examples

Two saved examples illustrating complementary failure modes. Prompts and model outputs below are reproduced verbatim from the experiment records. The examples use a fixed model and the same underlying probe within each comparison.

## Example 1: visual-only failure recovered by scaffolds

The question asks for the object's actual final location, so no belief attribution is required. The correct answer is **right**.

### Panel strip

![Example 1 panel strip](images/example1_panel_strip.png)

| Panel | Scene summary |
|---|---|
| 1 | Purple and orange are present; the pink object is near the left mint container and purple places it there. |
| 2 | Purple exits; orange remains; the pink object is in the left mint container. |
| 3 | Only orange is present; the pink object moves toward the right violet container. |
| 4 | Orange is present; the pink object is in the right violet container. |
| 5 | Purple returns; the pink object remains in the right violet container. |
| 6 | Both characters are present; the pink object remains in the right violet container. |

### Visual-only input (A)

**Prompt**

> Study this 6-panel visual sequence. Where is the pink object actually located in the final panel, left or right? Answer ONLY 'left' or 'right'.

**Model output**

> left

**Expected:** right  
**Result:** incorrect

### Perceptual scaffold (B_p)

**Prompt**

> Study this image. Here is a structured perceptual description: Panel 1: purple and orange characters are in the room. pink object is near the left mint container. purple character places the object there. Panel 2: purple character moves to the door and exits. orange character remains in the room. pink object is in the left mint container. Panel 3: Only orange character is in the room. pink object moves from the left mint container toward the right violet container. Panel 4: orange character is in the room. pink object is in the right violet container. Panel 5: purple character returns through the door. orange character is in the room. pink object is in the right violet container. Panel 6: purple and orange characters are both in the room. pink object is in the right violet container. Where is the pink object actually located in the final panel, left or right? Answer ONLY 'left' or 'right'.

**Model output**

> right

**Expected:** right  
**Result:** correct

### Full scaffold (B_f)

**Prompt**

> Study this image. Here is a full structured description: Panel 1: purple and orange characters are in the room. pink object is near the left mint container. purple character places the object there. Panel 2: purple character moves to the door and exits. orange character remains in the room. pink object is in the left mint container. Panel 3: Only orange character is in the room. pink object moves from the left mint container toward the right violet container. Panel 4: orange character is in the room. pink object is in the right violet container. Panel 5: purple character returns through the door. orange character is in the room. pink object is in the right violet container. Panel 6: purple and orange characters are both in the room. pink object is in the right violet container. purple character was outside when the object moved from left to right and did not see that move. Where is the pink object actually located in the final panel, left or right? Answer ONLY 'left' or 'right'.

**Model output**

> right

**Expected:** right  
**Result:** correct

### Text-only input (C)

**Prompt**

> purple and orange are in a room with a left mint container and a right violet container. purple places the pink object in the left container and then leaves. While purple is away, orange moves the object to the right container. purple returns after the move. Where is the pink object actually located in the final panel, left or right? Answer ONLY 'left' or 'right'.

**Model output**

> right

**Expected:** right  
**Result:** correct

The saved comparison shows a failure from pixels that is recovered when the transfer event is made explicit in the scaffold or text.

## Example 2: failure at the text-only ceiling

This is a text-only failure with the full ground-truth narration. The returning agent watched the object enter the right room before leaving, but the model answers **left**. The error over-applies an absent-agent/old-location heuristic instead of tracking what the agent witnessed.

### Panel strip

![Example 2 panel strip](images/example2_panel_strip.png)

| Event | Scene summary |
|---|---|
| 1 | Red starts in the left room with the cyan object; blue is in the right room. |
| 2 | Red carries the object into the right room while blue is watching. |
| 3 | Blue leaves. |
| 4 | While blue is gone, red places the object in the right brown container. |
| 5 | Blue returns. |

### Text-only input (C)

**Prompt**

> red starts in the left room with the cyan object. blue is in the right room. red carries the object into the right room while blue is watching. blue then leaves. While blue is gone, red places the object in the right brown container. blue returns later. Where does the blue character think the cyan object is, left or right? Answer ONLY 'left' or 'right'.

**Model output**

> left

**Expected:** right  
**Result:** incorrect

This case shows that the residual error is not limited to visual perception: text-side inference can also fail when the model must retain what an agent actually observed.
