# DeepModels

## RAFT-Stereo (Step by Step):

Consider for the following example RGB images of size (m, n, 3) = (128, 128, 3).

1. Receives two images of dimensions (m, n, 3) as input.
    *   image1 = torch.Size([1, 3, 128, 128])
    *   image2 = torch.Size([1, 3, 128, 128])
2. Computes features of size (m/4, n/4, 256)
    *   fmap1: torch.Size([1, 256, 32, 32])
    *   fmap2: torch.Size([1, 256, 32, 32])
3. Updates the Flow iteratively:
    *   Flow is defined by the tensor Coords: (m/4, n/4, 2)
        *   Coords0: torch.Size([1, 2, 32, 32])
        *   Coords1: torch.Size([1, 2, 32, 32])

**Correlation Volume:** <br>
*   For each iteration (Default is 32), we have:
    *   a (m/4, n/4, 9) correlation tensor per piramyd level.
*   That is, whether consider $iterations=2$, and a piramyd of $levels=4$, we have $2*4$ correlation matrices of dimension (m/4, n/4, 9).
*   The output of an iteration is a tensor OUT, that concatenates each level of the piramyd correlations, resulting an a dimensionality of (m/4, n/4, 9*levels). In the above example, OUT is (32, 32, 36)