## Training of Fast R-CNN
1. Hierarchical Sampling:
  - Sample mini-batch of N images. (N=2 used in the paper)
  - Sample R/N RoIs from each Image. (R=128 used in paper)
    - IoU (Intersection over union) with ground-truth bbox is used as filtering criteria.
2. Multi-task loss: $L(p,u,t^u,v) = L_{cls}(p,u) + \lambda [u \geq 1] L_{loc}(t^u,v)$
  - where, $p = [p_0, p_1, ..., p_{K-1}]$ is softmax over $K$ classes.
  - $u \in [0,1, ..., K-1]$ is the ground-truth class.
    - $u = 0$ for background class.
    - $[u \geq 1] = 0$ if $u=0$ else $1$. So $[u \geq 1] = 0$ is $0$ for background class and $1$ for other classes.
  - $t^u = [t_x^u, t_y^u, t_w^u, t_h^u]$ is translation & stretch of bbox wrt Object proposal.
    - $t_x^u = \frac{x - x_{op}}{w_{op}}$
    - $t_y^u = \frac{y - y_{op}}{w_{op}}$
    - $t_w^u = log(w/w_{op})$
    - $t_h^u = log(h/h_{op})$
    - where, $x, y, w, h$ is for the bbox and $x_{op}, y_{op}, w_{op}, h_{op}$ is for object proposal. 
  - $v = [v_x, v_y, v_w, v_h]$ is translation & stretch of ground-truth bbox wrt Object proposal.
    - $v_x = \frac{x_{gt} - x_{op}}{w_{op}}$
    - $v_y = \frac{y_{gt} - y_{op}}{w_{op}}$
    - $v_w = log(w_{gt}/w_{op})$
    - $v_h = log(h_{gt}/h_{op})$
    - where, $x_{gt}, y_{gt}, w_{gt}, h_{gt}$ is for the grount-truth bbox and $x_{op}, y_{op}, w_{op}, h_{op}$ is for object proposal. 
  - $L_{cls}(p,u) = -log(p[u])$
  - $L_{loc} = smooth_{L_1}(t^u - v)$
