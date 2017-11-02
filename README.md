# MyTooL-2
一套解决DOM中Node对象子节点和Element对象中子元素的关于页面兼容的问题
#### 我的思路是，子节点在IE8及之前的版本没有问题，而子元素在IE8之后没有问题，然后它们之间没有太大的差别，所以可以通过各自的优点来进行互补
```js
//查找第一个子节点或子元素的方法
function Firstchild(parent){
    var result;
    if(parent.firstChild.nodeType === 3 && /^\s+$/.test(parent.firstChild.nodeValue)){
        result = parent.firstElementChild; // 利用正则表达式来判断子节点是不是空白节点
    }else{
        result = parent.firstChild;
    }
    return result;
}
//查找最后一个子节点或子元素的方法
function Lastchild(parent){
    var result;
    if(parent.lastChild.nodeType === 3 && /^\s+$/.test(parent.lastChild.nodeValue)){
        result = parent.lastElementChild;
    }else{
        result = parent.lastChild;
    }
    return result;
}
//查找相邻兄弟中后一个兄弟的元素或节点
function Nbrother(name){
    var result;
    var someone = name.nextSibling;
    var otherone = name.nextElementSibling;
    if(someone.nodeType === 3 && /^\s+$/.test(someone.nodeValue)){
        result = otherone;
    }else{
        result = someone;
    }
    return result;
}
//查找相邻兄弟中前一个兄弟的元素或节点
function Pbrother(name){
    var result;
    var someone = name.previousSibling;
    var otherone = name.previousElementSibling;
    if(someone.nodeType === 3 && /^\s+$/.test(someone.nodeValue)){
        result = otherone;
    }else{
        result = someone;
    }
    return result;
}

// childElementCount - 获取子元素的个数存在兼容问题
// children - 可以获取所有的子元素，并且没有所谓的兼容问题
// childnodes - 可以获取所有的子节点，当然包含空白节点

//获取指定标签的所有子元素的个数
function Childrenum(parent){
    var result;
    var childsnum = parent.childElementCount;
    var childrens = parent.children.length;
    if(childsnum === undefined){
        result = childrens;
    }else{
        result = childsnum;
    }
    return result;
}
//获取指定标签的所有子节点
function Cnodes(parent){
    var children = parent.childNodes;
    for(i=0;i<children.length;i++){
        var child = children[i];
        if(child.nodeType === 3 && /^\s+$/.test(child.nodeValue)){
            parent.removeChild(child);
        }
    }
    return children;
}
```
