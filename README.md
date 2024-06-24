import { useState } from 'react';
import Select from 'react-select';
import "./Modal.css";

const postcodeOptions = [
  { value: "SW1A 1AA", label: "SW1A 1AA - Westminster" },
  { value: "E1 6AN", label: "E1 6AN - Shoreditch" },
  { value: "M1 1AE", label: "M1 1AE - Manchester" },
  { value: "E14 0HE", label: "E14 0HE - London Borough of Tower Hamlets" },
  // Add more postcode options as required
];

function Modal({ isOpen, onClose, onPostcodeApply, children }) {
  const [selectedPostcode, setSelectedPostcode] = useState(null);

  const handlePostcodeChange = (selectedOption) => {
    setSelectedPostcode(selectedOption);
  };

  const handleApplyClick = () => {
    onPostcodeApply(selectedPostcode ? selectedPostcode.value : "");
  };

  if (!isOpen) return null;

  return (
    <div className="modal-overlay">
      <div className="modal-content">
        <div className="postcode-section">
          <h4>Select Your UK Postcode</h4>
          <Select
            className="dropdown"
            value={selectedPostcode}
            onChange={handlePostcodeChange}
            options={postcodeOptions}
            placeholder="Select a postcode"
            isClearable
          />
          {selectedPostcode && <div className="selected-message">You selected: {selectedPostcode.label}</div>}
        </div>
        <button className="modal-close" onClick={onClose}>
          &times;
        </button>
        <button className="apply-button" onClick={handleApplyClick} disabled={!selectedPostcode}>
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
    "E14 0HE": "London Borough of Tower Hamlets",
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
    const localityName = await getLocalityFromPostcode(postcode);
    setPostcode(postcode);
    setLocality(localityName);
    setIsModalOpen(false);
  };

  return (
    <div className="main-container">
      <h2 className="advisor-heading">
        {advisorType} Advisor {locality && `(${locality})`}
      </h2>
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
