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









import { useState } from 'react';
import Select from "react-select";
import "./Modal.css";

function Modal({ isOpen, onClose, onLocalitySelect, children }) {
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
    onLocalitySelect(selectedOption);
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
        {children}
      </div>
    </div>
  );
}

export default Modal;

