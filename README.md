
var _cvs;
var prop;
var _loc;
var monitorJson={};
var paramenterJson={};
var monitorArray=new Array();
var canvas_x=1150;
var canvas_y=520;
var canvasTr;
var proportionNum=0;
var proportion=1;
var monitorData;
var suspension=false;

$(document).ready(function(){
	getProportion();
    getMonitorData();	
    initCanvasValue();
	drawTheMonitorImg();  	
});

function getProportion(){
	proportion=Math.pow(1.2,proportionNum);
}


function createCanvas(){
	canvasTr='<canvas id="myCanvas" ondrop="drop(event)" ondragover="allowDrop(event)"'+
	         'style="position.absolute;border:1px solid #c3c3c3;" width="'+canvas_x*proportion+'" height="'+canvas_y*proportion+'">'+
             '</canvas>'; 
	$('.mycanvas').empty();
	$('.mycanvas').append(canvasTr);
}

function initCanvasValue(){
	_cvs = document.getElementById("myCanvas");
    prop = {
    cvs:_cvs,
    width:_cvs.width,
    height:_cvs.height,
    ctx:_cvs.getContext("2d"),
    imgsheet:new Image()//显示结果的表
  };
  
  _cvs.onclick=function(e){
	e=e||event;
	_loc = _functions.winPos2CvsPos.call(_functions,_cvs, e.clientX, e.clientY);
	$.each(monitorData.monitor,function(i,list){
		if(_loc.x>=list.x*proportion&&_loc.x<=(list.x+list.width)*proportion&&_loc.y>=list.y*proportion&&_loc.y<=(list.y+list.height)*proportion){
		 window.location.href='monitorDetail.html';
       }	   
	});
}
 _cvs.onmousemove=function(e){
	e=e||event;
	_loc = _functions.winPos2CvsPos.call(_functions,_cvs, e.clientX, e.clientY);
	var flag=true;
	$.each(monitorData.monitor,function(i,list){
		if(_loc.x>=list.x*proportion&&_loc.x<=(list.x+list.width)*proportion&&_loc.y>=list.y*proportion&&_loc.y<=(list.y+list.height)*proportion){
		 //prop.ctx.rect(list.x*proportion-50,list.y*proportion-70,150,80);
         //prop.ctx.stroke();
		 prop.ctx.strokeRect(list.x*proportion-50,list.y*proportion-70,150,80);
		 prop.ctx.font='15px Arial';
         var txt='设备编号：'+list.name;
		 var txt='设备编号：'+list.name;
		 var txt='设备编号：'+list.name;
         prop.ctx.fillText(txt,list.x*proportion-50,list.y*proportion-50);
		 prop.ctx.fillText(txt,list.x*proportion-50,list.y*proportion-30);
		 prop.ctx.fillText(txt,list.x*proportion-50,list.y*proportion-10);		 
		 flag=false;
         suspension=true;	 
       }   
	});
	if(flag&&suspension){
	suspension=false;
	//createCanvas();
	//initCanvasValue();
	drawTheMonitorImg();
	}
}

}


function changCanvas(){
	createCanvas();
	initCanvasValue();
	
}

function allowDrop(ev)
{
ev.preventDefault();
}

function drag(ev)
{
ev.dataTransfer.setData("Text",ev.target.id);
}

function drop(ev)
{	
ev.preventDefault();
var data=ev.dataTransfer.getData("Text");
var srcimg=document.getElementById(data).src;
var img1=new Image();
img1.src=srcimg;

_loc = _functions.winPos2CvsPos.call(_functions,_cvs, ev.clientX, ev.clientY);

if(img1.src=='http://localhost:8080/webHtml/html/assets/img/monitor/tupian3.png'||img1.src=='http://localhost:8080/webHtml/html/assets/img/monitor/tupian2.png'){
	_loc.y=_loc.y+img1.height*(1-proportion);
	_loc.x=_loc.x+img1.width*(1-proportion);
}
prop.ctx.drawImage(img1,_loc.x,_loc.y,img1.width*proportion,img1.height*proportion);

//alert(img1.width+';'+img1.height+';'+_loc.x+';'+_loc.y);
$('#myModalInformation').modal('show');
paramenterToJson(_loc.x,_loc.y,img1.width,img1.height,srcimg); 
 clearNum();
//$('.create').empty();
}

   
var _functions = {
    //窗口坐标转为换cvs坐标
    winPos2CvsPos:function(cvs,_x,_y){
      var _box = cvs.getBoundingClientRect();//获得cvs元素相对于浏览器圆点的坐标
      return {
        x:_x-_box.left,
        y:_y-_box.top
      }
    },   
  }
  
/*$('.tupian').click(function(){
	var src=$(this).attr("src");
	var imgstr='<img id="drap1" src="'+src+'" draggable="true" ondragstart="drag(event)"/>';
	$('.create').empty();	
	$('.create').append(imgstr);
});*/

function paramenterToJson(x,y,width,height,src){
	paramenterJson['paramenter1']=$('#num1').val();
	paramenterJson['paramenter2']=$('#num2').val();
	paramenterJson['paramenter3']=$('#num3').val();	    
	paramenterJson['width']=width;
    paramenterJson['height']=height;
    paramenterJson['src']=src;	
	paramenterJson['x']=x/proportion;
	paramenterJson['y']=y/proportion;
	
	monitorArray.push(paramenterJson);
	paramenterJson={};
}

function clearNum(){
	$('#num1').val('');
    $('#num2').val('');
    $('#num3').val('');
}

$('.saveMap').click(function(){
	monitorJson['data']=monitorArray;
	alert(monitorJson);
});

$('.resetMap').click(function(){
	monitorArray=new Array();
	alert(monitorArray);
});

$('.amplifier').click(function(){
	proportionNum+=1;
    getProportion();	
	createCanvas();	
	initCanvasValue();
	drawTheMonitorImg();
});

$('.shrink').click(function(){
	proportionNum-=1;
	getProportion();
	createCanvas();
	initCanvasValue();
	drawTheMonitorImg();
});

function getMonitorData(){
	/*$.ajaxSettings.async=false;
	$.getJSON('ajax/data/monitorTopuData.txt',function(json){
		monitorData=json;
	});	
	$.ajaxSettings.async=true;*/
	monitorData=eval('('+dataJson+')');
}

function drawTheMonitorImg(){	  
	var img=new Image();
	var imgi;
	img.src=monitorData.background.src;
	img.onload=function(){
		prop.ctx.drawImage(this,0,0,canvas_x*proportion,canvas_y*proportion);		 
		$.each(monitorData.monitor,function(i,list){
			imgi=new Image();
			imgi.src=list.src;
			imgi.onload = function () {
			prop.ctx.drawImage(this,list.x*proportion,list.y*proportion,list.width*proportion,list.height*proportion);          		
		}  			
	});
	$.each(monitorArray,function(i,list){
		imgi=new Image();
		imgi.src=list.src;
		imgi.onload = function () {
		prop.ctx.drawImage(this,list.x*proportion,list.y*proportion,list.width*proportion,list.height*proportion);
		}		
	});
	
	};
}

$('.save').click(function(){
    var doupImage = new Image();
    doupImage.src = prop.ctx.toDataURL("image/png");
});


