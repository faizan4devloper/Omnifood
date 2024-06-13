.main-container{
  /*width: 600px;  */
  height: 100vh;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  display: flex;
}
.upload-container {
  position: absolute;
  top: 54%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, 0.5);
  width: 1050px;
  height: 400px;  
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
 
.uploadfile-container {
  background-color: #ccc;
  width: 250px;
  margin: auto;
  padding: 20px;
  /*border: 2px solid #000000;*/
        box-shadow: 0 0 20px rgba(0,0,0,0.5); 

  border-radius: 5px;
  text-align: center;
}
 
.upload-area {
  margin-bottom: 20px;
}
.upload-area h2{
  font-weight: 600;
  background: -webkit-gradient(
    linear,
    left top,
    right top,
    color-stop(-19.51%, #7abef7),
    color-stop(36.51%, #4080f5),
    to(#572ac2)
  );
  background: -webkit-linear-gradient(
    left,
    #7abef7 -19.51%,
    #4080f5 36.51%,
    #572ac2 100%
  );
  background: -o-linear-gradient(
    left,
    #7abef7 -19.51%,
    #4080f5 36.51%,
    #572ac2 100%
  );
  background: linear-gradient(
    90deg,
    #7abef7 -19.51%,
    #4080f5 36.51%,
    #572ac2 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
  text-transform: inherit !important;
  font-family: 'Poppins';
}
 
.upload-button {
  display: inline-block;
  padding: 10px 20px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s; /* Add transition effect */
}
 
.upload-button:hover {
  background-color: #0056b3;
}
 
/* Style the file input */
.file-input {
  display: none; /* Hide the file input */
}
 
/* Style the label for the file input */
.upload-button::before {
  content: "Choose File";
}
 
/* Optional: Adjust spacing between button text and icon */
.upload-button::after {
  content: "\1F4C2"; /* Unicode for file icon */
  margin-left: 8px; /* Adjust spacing */
}
 
.uploadfile-container.dragging {
  background-color: #f0f0f0;
  border-color: #999;
}
 
.file-list {
  text-align: left;
}
 
.file-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px 10px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 5px;
}
 
.file-name {
  flex: 1;
}
 
.file-remove {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
.back-header {
  position: absolute;
  display: flex;
  justify-content: center;
  left: 3%;
  top: 8%; 
}

.back-btn {
  padding: 15px 10px;
  width: auto; /* Changed to auto */
}
.review-container {
  background-color:#ccc;
  border-radius: 10px;
  width: 430px;
    margin: 30px;
    height: auto;
    padding: 20px;
      box-shadow: 0 0 20px rgba(0,0,0,0.5); 

    /*border:10px solid #fff;*/
}

.document-list {
  display: flex;
  flex-wrap: wrap;
}

.document {
  width: 430px;
  /*margin: 10px;*/
  /*padding: 10px;*/
  border: 1px solid #ccc;
}
.document h4{
  font-size: 12px;
  text-align: center;
}

.review-container h2{
  text-align: center;
font-weight: 600;
  background: -webkit-gradient(
    linear,
    left top,
    right top,
    color-stop(-19.51%, #7abef7),
    color-stop(36.51%, #4080f5),
    to(#572ac2)
  );
  background: -webkit-linear-gradient(
    left,
    #7abef7 -19.51%,
    #4080f5 36.51%,
    #572ac2 100%
  );
  background: -o-linear-gradient(
    left,
    #7abef7 -19.51%,
    #4080f5 36.51%,
    #572ac2 100%
  );
  background: linear-gradient(
    90deg,
    #7abef7 -19.51%,
    #4080f5 36.51%,
    #572ac2 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
  text-transform: inherit !important;
  font-family: 'Poppins';
}
/*.upload-container {*/
/*  position: relative;*/
/*}*/
