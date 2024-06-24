import { useState } from 'react';
import "./Modal.css";

function Modal({ isOpen, onClose, onPostcodeApply, children }) {
  const [postcode, setPostcode] = useState("");

  const handlePostcodeChange = (event) => {
    setPostcode(event.target.value);
  };

  const handleApplyClick = () => {
    onPostcodeApply(postcode);
  };

  if (!isOpen) return null;

  return (
    <div className="modal-overlay">
      <div className="modal-content">
        <div className="postcode-section">
          <h4>Enter Your UK Postcode</h4>
          <input
            type="text"
            value={postcode}
            onChange={handlePostcodeChange}
            placeholder="Enter postcode"
            className="postcode-input"
          />
        </div>
        <button className="modal-close" onClick={onClose}>
          &times;
        </button>
        <button className="apply-button" onClick={handleApplyClick} disabled={!postcode}>
          Apply
        </button>
        {children}
      </div>
    </div>
  );
}

export default Modal;







import React, { useState } from "react";
import { UploadedDoc } from "./UploadedDoc";
import { Chat } from "./Chat";
import { Insights } from "./Insights";
import Modal from "./Modal";

const getLocalityFromPostcode = async (postcode) => {
  // Mock response - replace this with an actual API call
  const postcodeToLocalityMap = {
    "SW1A 1AA": "Westminster",
    "E1 6AN": "Shoreditch",
    "M1 1AE": "Manchester",
    // Add more mappings as required
  };
  
  return postcodeToLocalityMap[postcode] || "Unknown locality";
};

function MainContainer({ advisorType }) {
  const [selectedQuestion, setSelectedQuestion] = useState(null);
  const [isModalOpen, setIsModalOpen] = useState(true);
  const [postcode, setPostcode] = useState("");
  const [locality, setLocality] = useState("");

  const handleQuestionClick = (question) => {
    setSelectedQuestion(question);
  };

  const handleSendQuestionInfo = (questionInfo) => {
    console.log("Question info sent to Chat:", questionInfo);
  };

  const handleCloseModal = () => {
    setIsModalOpen(false);
  };

  const handlePostcodeApply = async (postcode) => {
    setPostcode(postcode);
    const localityName = await getLocalityFromPostcode(postcode);
    setLocality(localityName);
    setIsModalOpen(false);
  };

  return (
    <div className="main-container">
      <h2 className="advisor-heading">
        {advisorType} Advisor {postcode ? `(${postcode})` : ''}
      </h2>
      {locality && <p className="locality-name">{locality}</p>}
      <UploadedDoc />
      <Chat onQuestionClick={handleQuestionClick} />
      <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
      
      <Modal isOpen={isModalOpen} onClose={handleCloseModal} onPostcodeApply={handlePostcodeApply}>
        {/* You can pass additional children here if needed */}
      </Modal>
    </div>
  );
}

export default MainContainer;
