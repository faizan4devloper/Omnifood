import React, { useState } from "react";
import "./Insights.css";

const Insights = ({ selectedSchool }) => {
  const [popupContent, setPopupContent] = useState(null);
  const [expandedSection, setExpandedSection] = useState(null);

  const handleExpand = (section) => {
    if (expandedSection === section) {
      setExpandedSection(null);
    } else {
      setExpandedSection(section);
    }
  };

  const handlePopup = (content) => {
    setPopupContent(content);
  };

  const closePopup = () => {
    setPopupContent(null);
  };

  return (
    <div className="insights-container">
      <h3>Insights</h3>
      {selectedSchool && (
        <div>
          <div className="section">
            <h4 onClick={() => handleExpand("parentReviews")}>
              Parent Reviews
              <span className="expand-icon">{expandedSection === "parentReviews" ? "▼" : "►"}</span>
            </h4>
            {expandedSection === "parentReviews" && (
              <div className="section-content">
                <p>Overall Rating - one liner</p>
                <button onClick={() => handlePopup("Review Summary")}>Review Summary (pop up)</button>
              </div>
            )}
          </div>
          <div className="section">
            <h4 onClick={() => handleExpand("ofstedRating")}>
              Ofsted Rating
              <span className="expand-icon">{expandedSection === "ofstedRating" ? "▼" : "►"}</span>
            </h4>
            {expandedSection === "ofstedRating" && (
              <div className="section-content">
                <textarea placeholder="Enter Ofsted Rating here..." rows={5}></textarea>
              </div>
            )}
          </div>
          <div className="section">
            <h4 onClick={() => handleExpand("admissionTrend")}>
              Admission Trend
              <span className="expand-icon">{expandedSection === "admissionTrend" ? "▼" : "►"}</span>
            </h4>
            {expandedSection === "admissionTrend" && (
              <div className="section-content">
                <p>Admissions: Enter admissions details here...</p>
                <p>Appeals: Enter appeals details here...</p>
              </div>
            )}
          </div>
          <div className="section">
            <h4 onClick={() => handleExpand("termPlan")}>
              Term Plan
              <span className="expand-icon">{expandedSection === "termPlan" ? "▼" : "►"}</span>
            </h4>
            {expandedSection === "termPlan" && (
              <div className="section-content">
                <button onClick={() => handlePopup("PDF link")}>PDF link (pop up view)</button>
              </div>
            )}
          </div>
        </div>
      )}
      {popupContent && (
        <div className="popup">
          <div className="popup-content">
            <h4>{popupContent}</h4>
            <button onClick={closePopup}>Close</button>
          </div>
        </div>
      )}
    </div>
  );
};

export default Insights;


.insights-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.section {
  margin-bottom: 20px;
  padding: 15px;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.section:hover {
  background-color: #f9f9f9;
}

.section h4 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 0;
  font-size: 18px;
}

.section-content {
  padding-top: 10px;
}

.popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup-content {
  background: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.popup-content h4 {
  margin-top: 0;
}

.popup-content button {
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.popup-content button:hover {
  background-color: #0056b3;
}

.expand-icon {
  font-size: 14px;
}
