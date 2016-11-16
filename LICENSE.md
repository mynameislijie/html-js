<!DOCTYPE html>
<html>
<head>
<title>monitorTopu</title>
<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="this is my page">
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    
    
     <link rel="stylesheet" type="text/css" href="assets/plugins/bootstrap/css/bootstrap.min.css">
	 <link rel="stylesheet" type="text/css" href="assets/plugins/bootstrapTree/tree.css">
	 <link rel="stylesheet" type="text/css" href="assets/css/style.css">
	 
	 <link rel="stylesheet" type="text/css" href="assets/css/monitorTopu.css">
  </head>
    
  <body>
 
    <!--顶层图片内容-->
    <div class="container-fluid top">
	
	<div class="row">
	  <div class="col-xs-12 head-top">
	    <div class="row">
		 <div class="col-xs-10"></div>
		 <div class="col-xs-2 user-container">
		    <div class="head-context">
			<label>登录用户：<label><label class="user">管理员</label>
			</div>
		 </div>
		</div>
	  </div>	
	</div>
	</div>
	 <!--顶层图片内容-->
	 
	 <!--间隔层-->
	<div class="container-fluid">
	<div class="row nav-top">
	<div class="col-xs-2 headIcon"></div>
	<div class="col-xs-5"><nav id="nav"></nav></div>
    <div class="col-xs-5" style="line-height:60px;text-align:right;">
    <font class="realTimer"></font>
    </div>
	</div>	
	</div>
	<!--间隔层-->

	
	
<!--View-->		
  <div class="container-fluid">
  <div class="row">
    	<div class="col-xs-2">
	    <div class="row">
		    <div class="col-xs-4"></div>
			<div class="col-xs-4 well"><img id="drap1" draggable="true" ondragstart="drag(event)" class="tupian" style="padding-left:10px"  src="assets/img/tupian1.png"/></div>			
			<div class="col-xs-4 well"><img id="drap2" draggable="true" ondragstart="drag(event)" style="padding-left:10px" src="assets/img/tupian3.png"/></div>	
		</div>	
		<div class="row">
		  <div class="col-xs-4"></div>
		  <div class="col-xs-8 well">
		    <img id="drap3" draggable="true" ondragstart="drag(event)" class="tupian" src="assets/img/tupian2.png"/>
		  </div>
		</div>
        <div class="row">
		<div class="col-xs-4"></div>
		  <div class="col-xs-8 well">
		    <img id="drap4" draggable="true" ondragstart="drag(event)" class="tupian" src="assets/img/tupian4.png"/>
		  </div>
		</div>
	    		
		<div class="row">
		 
		</div>
	</div>
	
	<div class="col-xs-8 well mycanvas">
    <div class="row">
     	
		<canvas id="myCanvas" ondrop="drop(event)" ondragover="allowDrop(event)"
		style="position.absolute;border:1px solid #c3c3c3;" width="1150" height="520">
		</canvas>
</div>
</div>
	  <div class="col-xs-1">
	    
	    <div class="row">		
		<div class="col-xs-8 well">
		<span><li class="glyphicon glyphicon-zoom-in amplifier form-control"></li></span>
		</div>
		</div>
		
		<div class="row">
        <div class="col-xs-8 well">
		<span><li class="glyphicon glyphicon-zoom-out shrink form-control"></li></span>
		</div>		
		</div>
		
		<div class="row">
        <div class="col-xs-8 well">
		<span><li class="glyphicon glyphicon-floppy-save save form-control"></li></span>
		</div>		
		</div>
		
		<div class="row">
        <div class="col-xs-8 well">
		 <input type="button" class="form-control saveMap" value="保存"/>
		</div>		
		</div>
		
		<div class="row">
        <div class="col-xs-8 well">
		 <input type="button" class="form-control resetMap" value="取消"/>
		</div>		
		</div>
		
	  </div>
	
	
	

  </div>

</div>
				
					
		<!--End View-->	

<div style="height:100px;"></div>
<!-- Start of Footer -->
			<div class="row">	
                 <div class="col-xs-12">			
			<img src="assets/img/bottom1.png" width="100%" height="100%"/>
			</div>
			</div>
<!-- End of Footer -->

<!--Modal-->
<div class="modal fade" id="myModalInformation" tabindex="-1" role="dialog" 
   aria-labelledby="myModalLabel" aria-hidden="true">
   <div class="modal-dialog">
      <div class="modal-content">
         <div class="modal-header">
            <button type="button" class="close" 
               data-dismiss="modal" aria-hidden="true">
                  &times;
            </button>
            <h4 class="modal-title" id="myModalLabelInformation">
               请填写具体的信息
            </h4>
         </div>
         <div class="modal-body InformationContext">
             <table class="table">
			<tbody>
			 <tr>
			    <td>参数1：</td>
				<td><input id="num1" type="text" class="form-control table-input"/></td>
			 </tr>
			 <tr>
			    <td>参数2：</td>
				<td><input id="num2" type="text" class="form-control table-input"/></td>
			 </tr>
			 <tr>
			    <td>参数3：</td>
				<td><input id="num3" type="text" class="form-control table-input"/></td>
			 </tr>
			 <tr>
			    <td></td>
				<td>
				<input type="button" class="btn btn-default reportAllProject" value="确认"/>
				<input type="button" data-dismiss="modal"  class="btn btn-primary" value="取消"/>
				</td>
			 </tr>
			 </tbody>
			</table>
         </div>
         
      </div><!-- /.modal-content -->
</div><!-- /.modal -->
	
	
	
	<!--plugins JS-->
	<script type="text/javascript" src="assets/plugins/jquery-2.1.1.min.js"></script><!-- jquery JS -->
	<script type="text/javascript" src="assets/plugins/bootstrap/js/bootstrap.min.js"></script><!-- Bootstrap JS-->
	<script type="text/javascript" src="assets/plugins/datatables/jquery.dataTables.min.js"></script><!-- dataTable JS -->
    <script type="text/javascript" src="assets/plugins/echarts.min.js"></script><!-- echarts JS -->
	<script type="text/javascript" src="assets/plugins/bootstrapTree/tree.js"></script><!-- echarts JS -->
	<!--plugins JS-->
	
	<!--page JS-->
	<script type="text/javascript" src="assets/js/commonScript.js"></script><!-- index JS-->
	<script type="text/javascript" src="assets/js/monitorTopu.js"></script><!-- index JS-->
	<script type="text/javascript" src="assets/js/dataValue.js"></script><!-- index JS-->
</body>
</html>
