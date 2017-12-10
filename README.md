# send
function sendFile(file) {
            var uri = "/index.php";
            var xhr = new XMLHttpRequest();
            var fd = new FormData();
            
           xhr.open("POST", uri, true);
           xhr.onreadystatechange = function() {
           if (xhr.readyState == 4 && xhr.status == 200) {
            var  txt = file.name;  
          var span = document.createElement('span');
          span.innerHTML = ['<p >'+txt+' <input type="checkbox"  checked="checked"/></p> '];
          document.getElementById('list').insertBefore(span, null);
		  }
            };
            fd.append('myFile', file);
            // Initiate a multipart/form-data upload
            xhr.send(fd);
        }window.onload = function() {
            var dropzone = document.getElementById("dropzone");
            dropzone.ondragover = dropzone.ondragenter = function(event) {
                event.stopPropagation();
                event.preventDefault();
            }
    
            dropzone.ondrop = function(event) {
                event.stopPropagation();
                event.preventDefault();

var filesArray = event.dataTransfer.files;
                for (var i=0; i<filesArray.length; i++) {
                    sendFile(filesArray[i]);
                }
            }
        }
