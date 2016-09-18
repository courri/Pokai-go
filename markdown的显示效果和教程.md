可以看一下[这个教程](http://www.bilibili.com/video/av3450195/)。


主要需要注意的是，代码的插入用的 ` 是Tab键上面的那个符号。


可以显示成这样： `我是一行之间的代码` ，这样是很常见的用法。


也可以首尾各用三个

matlab内置的生成WattsStrogatz小世界模型的 `WattsStrogatz.m` 文件，代码如下


``` matlab

function h = WattsStrogatz(N,K,beta)
% H = WattsStrogatz(N,K,beta) returns a Watts-Strogatz model graph with N
% nodes, N*K edges, mean node degree 2*K, and rewiring probability beta.
%
% beta = 0 is a ring lattice, and beta = 1 is a random graph.

% Connect each node to its K next and previous neighbors. This constructs
% indices for a ring lattice.
s = repelem((1:N)',1,K);
t = s + repmat(1:K,N,1);
t = mod(t-1,N)+1;

% Rewire the target node of each edge with probability beta
for source=1:N    
    switchEdge = rand(K, 1) < beta;
    
    newTargets = rand(N, 1);
    newTargets(source) = 0;
    newTargets(s(t==source)) = 0;
    newTargets(t(source, ~switchEdge)) = 0;
    
    [~, ind] = sort(newTargets, 'descend');
    t(source, switchEdge) = ind(1:nnz(switchEdge));
end

h = graph(s,t);
end

% Copyright 2015 The MathWorks, Inc.

```

其他的还是要去看看第一行的教程哦。
要看到这个markdown文件原来的代码，只需要点击右上的 *编辑(一个小铅笔)* 按钮即可哦。

此文件的名称是 `markdown的显示效果和教程.md`。
你的问文件名称也可以直接是代码。
比如 WattsStrogatz.m ，比如 HelloWorld.c 比如FirstJavaProgram.java ，都会高亮。
