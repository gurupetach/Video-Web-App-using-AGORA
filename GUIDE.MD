# Video Web App using Agora
 
This is a basic video chatting web app using Agora.io
## Requirements
- html/css/jS basics
- Agora account

## Hosted Demo ##
If you would like to see the demo in action, check out the [demo of the code in action](https://digitallysavvy.github.io/group-video-chat/) on GitHub Pages 

## How to Run the Demo ##
Start Xamp.
- Open the index file I have included 

If you want to test this out with friends use ngrok



1. Start new file and name it index.html
paste the code below

<html lang="en">
	<head>
		<title>Petach Agora Video Feed</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1">
	</head>
	<body>
		<div class="container-fluid p-0">
			<div id="main-container">
				<div id="screen-share-btn-container" class="col-2 float-right text-right mt-2">
					<button id="screen-share-btn"  type="button" class="btn btn-lg">
						<i id="screen-share-icon" class="fas fa-desktop"></i>
						share screen
					</button>
				</div>
				<div id="buttons-container" class="row justify-content-center mt-3">
					<div class="col-md-2 text-center">
						<button id="mic-btn" type="button" class="btn btn-block btn-dark btn-lg">
							<i id="mic-icon" class="fas fa-microphone" style="font-size:24px;color:red"></i>
							MICROPHONE
						</button>
					</div>
					<div class="col-md-2 text-center">
						<button id="video-btn"  type="button" class="btn btn-block btn-dark btn-lg">
							<i id="video-icon" class="fas fa-video"></i>
							VDEO
						</button>
					</div>
					<div class="col-md-2 text-center">
						<button id="exit-btn"  type="button" class="btn btn-block btn-danger btn-lg">
							<i id="exit-icon" class="fas fa-phone-slash"></i>
							END
						</button>
					</div>
				</div>
				<div id="full-screen-video"></div>
				<div id="lower-video-bar" class="row fixed-bottom mb-1">
					<div id="remote-streams-container" class="container col-9 ml-1">
						<div id="remote-streams" class="row">
							<!-- insert remote streams dynamically -->
						</div>
					</div>
					<div id="local-stream-container" class="col p-0">
						<div id="mute-overlay" class="col">
							<i id="mic-icon" class="fas fa-microphone-slash"></i>
						</div>
						<div id="no-local-video" class="col text-center">
							<i id="user-icon" class="fas fa-user"></i>
						</div>
						<div id="local-video" class="col p-0"></div>
					</div>
				</div>
			</div>
		</div>
    <div class="modal fade" id="modalForm">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header text-center">
            <h4 class="modal-title w-100 font-weight-bold">VIDEO JOIN FORM</h4>
            <button type="button" class="close" data-dismiss="modal">
              <span>&times;</span>
            </button>
          </div>
          <div class="modal-body mx-3">
            <div class="md-form mb-4">
              <input type="text" id="form-appid" placeholder="ID by Agora" class="form-control">
              <label for="form-appid">Enter App ID </label>
            </div>
            
            <div class="md-form mb-4">
			  <input type="text" id="form-channel" placeholder="Agora Channel name" class="form-control">
			  
              <label for="form-channel">Enter Channel Name</label>
            </div>
            
          </div>
          <div class="modal-footer d-flex justify-content-center">
            <button id="join-channel" class="btn btn-primary btn-lg btn-block">JOIN</button>
          </div>
        </div>
      </div>
    </div>
	</body>
	<script src="AgoraRTCSDK-3.3.1.js"></script>
	<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.7.0/css/all.css" integrity="sha384-lZN37f5QGtY3VHgisS14W3ExzMWZxybE1SJSEsQp9S+oqd12jhcu+A56Ebc1zFSJ" crossorigin="anonymous">
	<link href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css" rel="stylesheet">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/js/bootstrap.min.js"></script>
	<script type="text/javascript">
		$("#mic-btn").prop("disabled", true);
		$("#video-btn").prop("disabled", true);
		$("#screen-share-btn").prop("disabled", true);
		$("#exit-btn").prop("disabled", true);

		$(document).ready(function(){
			$("#modalForm").modal("show");
		});
	</script>
	<script type="text/javascript">
		// init the session when user clicks join btn
		$( "#join-channel" ).click(function( event ) {
			var agoraAppId = $('#form-appid').val();
			var token = $('#form-token').val();
			var channelName = $('#form-channel').val();
			var uid = parseInt($("#form-uid").val());
			$("#modalForm").modal("hide");
			initClientAndJoinChannel(agoraAppId, token, channelName, uid);
		});
	</script>
	
	<script src="ui.js"></script>
	<script src="agora-interface.js"></script>
	<link rel="stylesheet" type="text/css" href="style.css"/>
</html>



2. make a new file and save it as style.css

paste the code below to it


#buttons-container {
  position: absolute;
  z-index: 2;  
  width: 100vw;
}

#full-screen-video {
  position: absolute;
  width: 100vw;
  height: 100vh;
}

#lower-video-bar {
  height: 20vh;
}

#local-stream-container { 
  position: relative; 
  display: inline-block;
}

.remote-stream-container { 
  display: inline-block;
}

#remote-streams {
  height: 100%;
}

#local-video {
  position: absolute;
  z-index: 1;
  height: 20vh;
  max-width: 100%;
}

.remote-video {
  position: absolute;
  z-index: 1;
  height: 100% !important;
  width: 80%;
  max-width: 500px;
}

#mute-overlay {
  position: absolute;
  z-index: 2;
  bottom: 0;
  left: 0;
  color: #d9d9d9;
  font-size: 2em;
  padding: 0 0 3px 3px;
  display: none;
} 

.mute-overlay {
  position: absolute;
  z-index: 2;
  top: 2px;
  color: #d9d9d9;
  font-size: 1.5em;
  padding: 2px 0 0 2px;
  display: none;
}

#no-local-video, .no-video-overlay {
  position: absolute;
  z-index: 3;
  width: 100%;
  top: 40%;
  color: #cccccc;
  font-size: 2.5em;
  margin: 0 auto;
  display: none;
}

.no-video-overlay {
  width: 80%;
}

#screen-share-btn-container {
  z-index: 99;
  color: red;
}



Done
Just isert AGORA APP ID and CHANNEL NAME
