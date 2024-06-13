import React, { useState } from "react";
import "./App.css"
import { BrowserRouter, Routes, Route } from "react-router-dom";

import { Header } from "./components/Landing/Header";
import { Hero } from "./components/Landing/Hero"; 
import { NewClaimPage } from "./NewClaimPage";
import { Footer } from "./components/Landing/Footer";


function App() {
  const [selectedDocument, setSelectedDocument] = useState(null);

  const handleDocumentSelect = (document) => {
    setSelectedDocument(document);
  };

  return (
    <BrowserRouter>
      <Header />
      
      <Routes>
        <Route path="/" element={
          <Hero onDocumentSelect={handleDocumentSelect} />
        } />
        
        <Route path="/NewClaimPage" element={
          <NewClaimPage />  
        } />
      </Routes>
      
      <Footer />
    </BrowserRouter>
  );
}

export default App;

import React, { useState } from "react";
import {useNavigate } from "react-router-dom";
import "./NewClaimPage.css";
 
export function NewClaimPage() {
  const [dragging, setDragging] = useState(false);
  const [files, setFiles] = useState([]);
  const [reviewFiles, setReviewFiles] = useState([]);

  const handleReviewFile = (file) => {
    setReviewFiles(prev => [...prev, file]);
  }
 
  const handleDragEnter = (e) => {
    e.preventDefault();
    setDragging(true);
  };
 
  const handleDragLeave = (e) => {
    e.preventDefault();
    setDragging(false);
  };
 
  const handleDragOver = (e) => {
    e.preventDefault();
    setDragging(true);
  };
 
  const handleDrop = (e) => {
    e.preventDefault();
    setDragging(false);
    const droppedFiles = Array.from(e.dataTransfer.files);
    handleFiles(droppedFiles);
  };
 
  const handleFiles = (newFiles) => {
    const filesArray = Array.from(newFiles);
 
    const updatedFiles = filesArray.map((file) => ({
      file: file,
      id: Math.random().toString(36).substr(2, 9), // generate a unique ID for each file
    }));
 
    setFiles((prevFiles) => [...prevFiles, ...updatedFiles]);
  };
 
  const handleFileRemove = (id) => {
const updatedFiles = files.filter((file) => file.id !== id);
    setFiles(updatedFiles);
  };
 
 const fileItems = files.map((file)=>(
   <div className="file-item" key={file.id}>
   <span className="file-name">{file.file.name}</span>
   <button className="file-remove" onClick={()=> handleFileRemove(file.id)}>Remove</button>
   </div>
   ));
   
     const navigate = useNavigate();
     
    // pr

  return (
    <div className="main-container">
<div className="back-header">
      <a className="back-btn"  onClick={() => navigate(-1)}>back</a>
      <h2>Upload & Preview Documents</h2>
</div>
      <div className="upload-container">
              

      <div
        className={`uploadfile-container ${dragging ? "dragging" : ""}`}
        onDragEnter={handleDragEnter}
        onDragOver={handleDragOver}
        onDragLeave={handleDragLeave}
        onDrop={handleDrop}
      >
        <div className="upload-area">
          <h2>Drag & Drop Files Here</h2>
          <p>or</p>
          <input
            type="file"
            id="fileInput"
            className="file-input"
            onChange={(e) => handleFiles(e.target.files)}
            multiple
          />
          <label htmlFor="fileInput" className="upload-button">
            Select Files
          </label>
        </div>
        <div className="file-list">{fileItems}</div>
      </div>
    <div className="review-container">
        <h2>Review Documents</h2>
        <div className="document-list">
          {files.map((file,index) => (
            <div key={file.id} className="document">
              <h4>{index+1}. {file.file.name}</h4> 
            </div>
          ))}
        </div>
      </div>
    </div>
    </div>
  );
}

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

import React, { useState, useEffect } from "react";
import ReactDOM from "react-dom/client";
import { useNavigate} from "react-router-dom";
import { Document, Page } from "react-pdf";
import Select from "react-select";
// import  NewClaimPage  from "./NewClaimPage"
import "./Hero.css";

export function Hero({ onDocumentSelect }) {
  const [claimType, setClaimType] = useState("");
  const navigate = useNavigate();
  const [documents, setDocuments] = useState([]);
  const [selectedDocUrl, setSelectedDocUrl] = useState("");

const handleClaimTypeChange = (e) => {
    setClaimType(e.target.value);
    if (e.target.value === "new") {
      navigate("./NewClaimPage"); 
    }
  }
  
  // Mock function to fetch documents
  const fetchDocuments = () => {
    // This could be replaced with an actual API call
    return new Promise((resolve, reject) => {
      // Simulating an API call with setTimeout
      setTimeout(() => {
        const mockDocuments = [
          {
            name: "Document 1",
            url: "https://css4.pub/2017/newsletter/drylab.pdf",
          },
          {
            name: "Document 2",
            url: "https://css4.pub/2017/newsletter/drylab.pdf",
          },
          {
            name: "Document 3",
            url: "https://css4.pub/2017/newsletter/drylab.pdf",
          },
        ];
        resolve(mockDocuments);
      }, 1000); // Simulating a 1 second delay
    });
  };

  useEffect(() => {
    fetchDocuments().then((data) => {
      setDocuments(data);
    });
  }, []);

  // const handleDocumentSelect = (event) => {
  //   const selectedUrl = event.target.value;
  //   const selectedDoc = documents.find((doc) => doc.url === selectedUrl);
  //   setSelectedDocUrl(selectedDoc.url);
  //   onDocumentSelect(selectedDoc);
  // };
  const handleDocumentSelect = (selected) => {
    const selectedDoc = documents.find(doc => doc.name === selected.value);
    setSelectedDocUrl(selectedDoc.url);
    onDocumentSelect(selectedDoc);
  }  

  return (
    <div className="hero">
      <div className="hero-content">
        <div className="claim-info">
          <h1>iAssure Claim.</h1>
          <p>
           Empower your claim process to minimize Claim Denial and maximize reimbursements.
          </p>
        </div>
        <div className="claim-form">
          <form>
            <h2>Submit Your Claim</h2>
            <div className="form-group">
              <label>Claim Documents</label>
            </div>
            <div className="form-group">
              <label>Type of Claim:</label>
              <div>
                <label>
                  <input
                    type="radio"
                    value="new"
                    checked={claimType === "new"}
                    // onChange={(e) => setClaimType(e.target.value)}
                    // onClick={()=> navigate('/new-claim')}
                    onChange={handleClaimTypeChange} 

                  />
                  New
                </label>
                <label>
                  <input
                    type="radio"
                    value="existing"
                    checked={claimType === "existing"}
                    onChange={(e) => setClaimType(e.target.value)}
                  />
                  Existing
                </label>
              </div>
            </div>
            {claimType === "existing" && (
              <div className="form-group">
                <label>Select Existing Claim</label>
                <Select 
      options={documents.map(doc => ({value: doc.name, label: doc.name}))}
      onChange={handleDocumentSelect}
    />
              </div>
            )}
            {selectedDocUrl && (
              <div className="pdf-container">
                <Document file={selectedDocUrl}>
                  <Page pageNumber={1} />
                </Document>
              </div>
            )}
          </form>
        </div>
      </div>
    </div>
  );
}
