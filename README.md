%此函数为非负矩阵分解的迭代算法
function [W,H]=NMF(V,r)
%V是原图像组，为n*m，n是每张图像素数，m是图像数，r是特征数
%V=W*H，W是基向量矩阵，H是在基下的坐标向量
sizeV=size(V);
n=sizeV(1);
m=sizeV(2);
W=abs(rand(n,r));
H=abs(rand(r,m));
for iterate=1:100
    WV=W'*V;
    WWH=W'*W*H;
    for a=1:r
        for u=1:m
            H(a,u)=H(a,u)*WV(a,u)/WWH(a,u);
        end
    end
    VH=V*H';
    WHH=W*H*H';
    for i=1:n
        for a=1:r
            W(i,a)=W(i,a)*VH(i,a)/WHH(i,a);
        end
    end
end
