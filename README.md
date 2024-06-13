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
