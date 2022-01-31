## FAST: Feature from Accelerated Segment Test
- The original segment test criterion operates by considering a circle of sixteen pixels around the corner candidate p.
- The detector classifies p as a corner if there exists a set of n contiguous pixels in the circle which are:
    - all brighter then that the intensity of the candidate pixel $I_p$ plus a threshold.
    - or all darker then $I_p - t$

- This detector in itself exhibits high performance, but there are several weaknesses:
    1. The high-speed test does not generalise well for $n < 12$.
    2. The choice and ordering of the fast test pixels contains implicit assumptions about the distribution of feature appearance.
    3.  Knowledge from the first 4 tests is discarded.
    4. Multiple features are detected adjacent to one another.

## Machine Learning a Corner Detector
- Presents approach to address the first three points.

The process operates in two stages:
1. For a given n, first, corners are detected from a set of images using the segment test criterion for n and a convenient threshold.
  1.1. This uses a slow algorithm which for each pixel simply test all 16 locations on the circle around it.
  1.2. For each location on the circle $x \in \{1..16\}$, the pixel at that position relative to p(denoted by $p_x$) can have one of three state $S_{px}$:
    1.2.1. darker if $I_{p_x} \leq I_p - t$
    1.2.2. similar $I_p - t < I_{p_x} < I_p + t$
    1.2.3. brighter if $I_{p_x} \geq I_p + t$
  1.3. Choosing an x and computing $S_{px}$ for all $p \in P$ partitions P into three subsets:
    1.3.1. $P_d$
    1.3.2. $P_s$
    1.3.3. $P_b$
  1.4. Let $K_p$ be a boolean variable which is true if p is a corner and false othrewise.
2. Select x which yields the most information about wether the candidate pixel is a corner, measured by the entropy of $K_p$
  2.1. The entropy of K for the set P is:
    2.1.1. $H(P) = (c + \bar{c})log_2(c + \bar{c}) - clog_2c - \bar{c}log_2\bar{c}$
    2.1.2. where. $c = | \{p|K_p is true\}|$ (number of corners)
    2.1.3. where. $\bar{c} = | \{p|K_p is false\}|$ (number of non corners)
  2.2. The choice of x then yield the information gain:
    2.2.1. $H(P) - H(P_d) - H(P_s) - H(P_b)$

