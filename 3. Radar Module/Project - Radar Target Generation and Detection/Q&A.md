# Implementation steps for the 2D CFAR process:

I implemented the 2D CFAR as per the guide provided throughout the lesson. To reiterate the steps:

1. Determine the number of Training and Guard Cells in both the range and doppler axis: Tr, Td, Gr, and Gd respectively.
2. Selection of the grid that includes training, guard and test cells took some experimentation as did not want a grid too small or too large. Configuring the parameters of guard size and training size was also from observing several samples to make sure there were enough guard cells to not cause leaking and not too many training cells to make it excessive.
3. Slide the grid across the Range-Doppler Map to measure and average the noise across the training cells to obtain the threshold.
4. I added a small offset to the threshold to eliminate some noise that made it through the barrier.
5. Then I parsed the values and assigned 1s or 0s accordingly to get a more clean looking representation.

# Selection of Training, Guard Cells and Offset

I based the selection of Training Cells, Guard Cells, and Offset manly after observing visual graphs of the signal as simply knowing the size of the Range-Doppler Map is not enough to check for leaking or proper grid selection that includes the training, guard and offset params. The Training Cells you could infer cannot be too large since we want to maintain a resolution of 1m, so several design restrictions did come into play.

# Steps taken to suppress the non-thresholded cells at the edges

Naturally since we cannot get the Cells Under Test to be evaluated at the edges due to the training cells occupying that space, after parsing for target signals and setting them to 1s and other noise values to 0, the remaining values that were neither 0 or 1 were assigned 0 as well.