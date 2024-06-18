import React, { useState } from "react";
import { useNavigate } from "react-router-dom";
import "./NewClaimPage.css";
import { Modal } from "./components/Landing/Modal";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faChevronRight } from "@fortawesome/free-solid-svg-icons";

export function NewClaimPage() {
  const [dragging, setDragging] = useState(false);
  const [files, setFiles] = useState([]);
  const [selectedFile, setSelectedFile] = useState(null); // State for selected file for preview
  const [showModal, setShowModal] = useState(false); // State to control modal visibility
  const [isSubmitted, setIsSubmitted] = useState(false);

  const navigate = useNavigate();

  const handleSubmit = () => {
    // Call API or handle form submission
    setIsSubmitted(true); 

    // Navigate to the SummaryView component after submission
    navigate("/summary");
  };

  const handleDragEnter = (e) => {
    e.preventDefault();
    e.stopPropagation();
    setDragging(true);
  };

  const handleDragLeave = (e) => {
    e.preventDefault();
    e.stopPropagation();
    setDragging(false);
  };

  const handleDragOver = (e) => {
    e.preventDefault();
    e.stopPropagation();
    setDragging(true);
  };

  const handleDrop = (e) => {
    e.preventDefault();
    e.stopPropagation();
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

  const handlePreview = (file) => {
    setSelectedFile(file);
    setShowModal(true);
  };

  const fileItems = files.map((file) => (
    <div className="file-item" key={file.id}>
      <span className="file-name">{file.file.name}</span>
      <button className="file-remove" onClick={() => handleFileRemove(file.id)}>Remove</button>
    </div>
  ));

  return (
    <div className="main-container">
      <button className="back-btn" onClick={() => window.history.back()}>
        Landing <FontAwesomeIcon icon={faChevronRight} />
      </button>
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
              Browse
            </label>
          </div>
          <div className="file-list">{fileItems}</div>
        </div>
        <div className="review-container">
          <h2>Review Documents</h2>
          <div className="document-list">
            {files.map((file, index) => (
              <div key={file.id} className="document">
                <h4 onClick={() => handlePreview(file.file)}>
                  {index + 1}. {file.file.name}
                </h4>
              </div>
            ))}
          </div>
          <button onClick={handleSubmit} className="submit-btn">Submit</button>
        </div>
      </div>
      <Modal show={showModal} onClose={() => setShowModal(false)}>
        {selectedFile && (
          <div className="modal-content">
            <button className="modal-close" onClick={() => setShowModal(false)}>
              &times;
            </button>
            <h2>{selectedFile.name}</h2>
            {selectedFile.type.startsWith("image/") ? (
              <img
                src={URL.createObjectURL(selectedFile)}
                alt={selectedFile.name}
              />
            ) : (
              <iframe
                src={URL.createObjectURL(selectedFile)}
                width="100%"
                height="400px"
                title="file-preview"
              />
            )}
          </div>
        )}
      </Modal>
    </div>
  );
}















App___________-_-_-_-_-_-_-__-

