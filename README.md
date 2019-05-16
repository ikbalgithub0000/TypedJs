# TypedJs
function $(target){
return document.getElementById(target) || document.getElementsByClassName(target);
}
function atribut(target,atribut){
return target.getAttribute(atribut)
}

var record = new Object();
record.list = 0;
record.charx = 0;

function cek(string,target){
if(target.textContent.length<1){
target.setAttribute("data-state","autotype")
}
else if(target.textContent.length == string.length){
target.setAttribute("data-state","delete")
}
}

function listnext(array,string,target){
if(target.textContent.length<1 && record.list<array.length-1){ record.list = record.list + 1}
else if(target.textContent.length<1 && record.list == array.length-1){ record.list = 0 }
}

function autotype(string,target){
target.textContent = target.textContent + string[record.charx];
record.charx = record.charx + 1;
}

function reset(target){
let chn = target.textContent.slice(0,-1);
target.textContent = chn;
record.charx = record.charx - record.charx;
}

function begin(array,target){
this.string = array[record.list]
switch(atribut(target,"data-state")){
case "autotype" :
autotype(string,target);
cek(string,target)
break;
case "delete" :
cek(string,target);
listnext(array,string,target);
reset(target);
break;
}
}

