<div class="form-group "><label class="col-sm-3 control-label" for="photograph">Upload Photograph        </label>    <div class="col-sm-9 controls">
<input type="file" name="photograph" value="" accept="image/jpeg" id="photograph" class="form-control" data-target="#confirmStep5" data-toggle="modal"><span class="help-block">Upload a 3.5 cm x 4.5 cm (width x height) photograph in JPEG/JPG format with maximum pixel resolution 480 x 640 and minimum pixel resolution 240 x 320. Aspect ratio (width : height) has to be between 0.6603 and 0.8933.</span>
</div>
</div>

<div class="modal fade" id="confirmStep5" tabindex="-1" role="dialog" aria-labelledby="modalLabel5" aria-hidden="true">
	<div class="modal-dialog modal-lg">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal">
					<span aria-hidden="true">×</span><span class="sr-only">Close</span>
						</button>
						<h4 class="modal-title" id="modalLabel1">Crop the image</h4>
			</div>
			<div class="modal-body">
				<div class="container">
					<div class="row">
						<div class="span12">
							<div class="jc-demo-box">
							   <img src="#" id="target" alt="[photo image]">
							   <canvas id="preview" style="width:50px;height:50px;overflow:hidden;"> </canvas>
							</div>
							<br>
							<button type="button" data-dismiss="modal" class="btn btn-primary" id="continueStep1">Skip cropping</button>
							<button type="button" data-dismiss="modal" class="btn btn-primary" id="continueStep1">Crop and Upload</button>
							<button type="button" class="btn btn-default" id="clear_selection">Clear the selection</button>
					   	
					</div>
				</div>
			</div>

		</div>
	</div>
</div>
<script type="text/javascript">
  jQuery(function($){
	 
    var api;

    $('#target').Jcrop({
      // start off with jcrop-light class
      bgOpacity: 0.5,
      keySupport: false,
      bgColor: 'black',
      minSize:[240,320],
      maxSize:[480,640],
     /* onChange : updatePreview,
      onSelect : updatePreview, */
      height:160,
      width:120,
      addClass: 'jcrop-normal'
    },function(){
      api = this;
      api.setSelect([0,0,240,320]);
      api.setOptions({ bgFade: true });
      api.ui.selection.addClass('jcrop-selection');
    });

  });
 
  jQuery('#clear_selection').click(function(){
	  $('#target').Jcrop({    
		  
	      setSelect: [0,0,0,0],
	    });
	});
 
   function readURL(input) {
		
	    if (input.files && input.files[0]) {
	        var reader = new FileReader();
	        reader.onload = function (e) {
	            $('#target').attr('src', e.target.result);
	            setProperties();       
	        }
	        reader.readAsDataURL(input.files[0]);
	    }
	}
	
   function setProperties(){
	   $('#target').Jcrop({       	
	  	    	  setSelect: [0,0,240,320]
	  	    }); 
   }
	$("#photograph").change(function(){
	    readURL(this);	   
	});
  
	function make_base() {
		console.log("make_base called");
	    var base_image = new Image();
	    base_image.src = '';
	    base_image.onload = function () {
	        context.drawImage(base_image, 0, 0);
	    }
	}

	var canvas = document.getElementById('preview'),
	context = canvas.getContext('2d');

	make_base();
	function updatePreview(c) {
		console.log("called");
	    if(parseInt(c.w) > 0) {
	        // Show image preview
	        var imageObj = $("#target")[0];
	        var canvas = $("#preview")[0];
	        var context = canvas.getContext("2d");
	        context.drawImage(imageObj, c.x, c.y, c.w, c.h, 0, 0, canvas.width, canvas.height);
	    }
	};
	

</script>
