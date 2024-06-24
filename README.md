import { useState } from 'react';
import Select from "react-select";
import "./Modal.css";

function Modal({ isOpen, onClose, onLocalityApply, children }) {
  const [localities] = useState([
    { value: "England", label: "England" },
    { value: "Los Angeles", label: "Los Angeles" },
    { value: "Chicago", label: "Chicago" },
    { value: "Houston", label: "Houston" },
    { value: "Phoenix", label: "Phoenix" }
  ]);
  
  const [selectedLocality, setSelectedLocality] = useState(null);
  
  const handleLocalityChange = (selectedOption) => {
    setSelectedLocality(selectedOption);
  };
  
  const handleApplyClick = () => {
    onLocalityApply(selectedLocality);
  };

  if (!isOpen) return null;

  return (
    <div className="modal-overlay">
      <div className="modal-content">
        <div className="locality-section">
          <h4>Choose Your Locality</h4>
          <Select
            className="dropdown"
            value={selectedLocality}
            onChange={handleLocalityChange}
            options={localities}
            placeholder="Select a locality"
            isClearable
          />
          {selectedLocality && <div className="selected-message">You selected: {selectedLocality.label}</div>}
        </div>
        <button className="modal-close" onClick={onClose}>
          &times;
        </button>
        <button className="apply-button" onClick={handleApplyClick} disabled={!selectedLocality}>
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

function MainContainer({ advisorType }) {
  const [selectedQuestion, setSelectedQuestion] = useState(null);
  const [isModalOpen, setIsModalOpen] = useState(true);
  const [selectedLocality, setSelectedLocality] = useState(null);

  const handleQuestionClick = (question) => {
    setSelectedQuestion(question);
  };

  const handleSendQuestionInfo = (questionInfo) => {
    console.log("Question info sent to Chat:", questionInfo);
  };

  const handleCloseModal = () => {
    setIsModalOpen(false);
  };

  const handleLocalityApply = (locality) => {
    setSelectedLocality(locality);
    setIsModalOpen(false);
  };

  return (
    <div className="main-container">
      <h2 className="advisor-heading">
        {advisorType} Advisor {selectedLocality ? `(${selectedLocality.label})` : ''}
      </h2>
      <UploadedDoc />
      <Chat onQuestionClick={handleQuestionClick} />
      <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
      
      <Modal isOpen={isModalOpen} onClose={handleCloseModal} onLocalityApply={handleLocalityApply}>
        {/* You can pass additional children here if needed */}
      </Modal>
    </div>
  );
}

export default MainContainer;
