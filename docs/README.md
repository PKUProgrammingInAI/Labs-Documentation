# 北大人工智能中的编程课程文档
欢迎各位同学选修人工智能中的编程!

在本课程中, 你将最终实现一个类似于pytorch的深度学习框架, 可以使用gpu强大的并行能力去训练你自己的神经网络. 

同时, 你也将体验不一样的并行程序, 比如你将会看到下面这样神奇的程序: 
```cuda
__global__ void relu_gpu(float* in, float* out) {
    int i = threadIdx.x;
    out[i] = in[i] > 0 ? in[i] : 0;
}
relu_gpu<<<1, N>>>(d_in, d_out);
```
在学习的过程中, 你将会和他们持续性打交道. 

## TODO
- [x] 问答墙
- [ ] 环境配置
- [ ] lab指导
