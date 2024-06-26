<div className="section">
            <h4 onClick={() => handleExpand("ofstedRating")}>
              <span className="expand-icon">
                {expandedSection === "ofstedRating" ? (
                  <FontAwesomeIcon icon={faAngleRight} />
                ) : (
                  <FontAwesomeIcon icon={faAngleDown} />
                )}
              </span>
              Ofsted Rating
            </h4>
            {expandedSection === "ofstedRating" && (
              <div className="section-content">
                <textarea
                  placeholder="Enter Ofsted Rating here..."
                  rows={5}
                ></textarea>
              </div>
            )}
          </div>
import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faAngleRight, faAngleDown } from "@fortawesome/free-solid-svg-icons";
import "./Insights.css";

export function Insights({ selectedSchool }) {
  const [popupContent, setPopupContent] = useState(null);
  const [expandedSection, setExpandedSection] = useState(null);
  const [ofstedRating, setOfstedRating] = useState("");
  const [reportText, setReportText] = useState("");

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
      <h3>Insights : {selectedSchool}</h3>
      {selectedSchool && (
        <div>
          <div className="section">
            <h4 onClick={() => handleExpand("parentReviews")}>
              <span className="expand-icon">
                {expandedSection === "parentReviews" ? (
                  <FontAwesomeIcon icon={faAngleRight} />
                ) : (
                  <FontAwesomeIcon icon={faAngleDown} />
                )}
              </span>
              Parent Reviews
            </h4>
            {expandedSection === "parentReviews" && (
              <div className="section-content">
                <p>Overall Rating - one liner</p>
                <button onClick={() => handlePopup("Review Summary")}>
                  Review Summary (pop up)
                </button>
              </div>
            )}
          </div>
          <div className="section">
            <h4 onClick={() => handleExpand("ofstedRating")}>
              <span className="expand-icon">
                {expandedSection === "ofstedRating" ? (
                  <FontAwesomeIcon icon={faAngleRight} />
                ) : (
                  <FontAwesomeIcon icon={faAngleDown} />
                )}
              </span>
              Ofsted Rating
            </h4>
            {expandedSection === "ofstedRating" && (
              <div className="section-content">
                <div className="rating-select">
                  <label>
                    <input
                      type="radio"
                      name="ofstedRating"
                      value="Inadequate"
                      checked={ofstedRating === "Inadequate"}
                      onChange={(e) => setOfstedRating(e.target.value)}
                    />
                    Inadequate
                  </label>
                  <label>
                    <input
                      type="radio"
                      name="ofstedRating"
                      value="Satisfactory"
                      checked={ofstedRating === "Satisfactory"}
                      onChange={(e) => setOfstedRating(e.target.value)}
                    />
                    Satisfactory
                  </label>
                  <label>
                    <input
                      type="radio"
                      name="ofstedRating"
                      value="Good"
                      checked={ofstedRating === "Good"}
                      onChange={(e) => setOfstedRating(e.target.value)}
                    />
                    Good
                  </label>
                  <label>
                    <input
                      type="radio"
                      name="ofstedRating"
                      value="Outstanding"
                      checked={ofstedRating === "Outstanding"}
                      onChange={(e) => setOfstedRating(e.target.value)}
                    />
                    Outstanding
                  </label>
                </div>
                <textarea
                  placeholder="Enter Ofsted Rating report here..."
                  rows={5}
                  value={reportText}
                  onChange={(e) => setReportText(e.target.value)}
                ></textarea>
              </div>
            )}
          </div>
          <div className="section">
            <h4 onClick={() => handleExpand("admissionTrend")}>
              <span className="expand-icon">
                {expandedSection === "admissionTrend" ? (
                  <FontAwesomeIcon icon={faAngleRight} />
                ) : (
                  <FontAwesomeIcon icon={faAngleDown} />
                )}
              </span>
              Admission Trend
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
              <span className="expand-icon">
                {expandedSection === "termPlan" ? (
                  <FontAwesomeIcon icon={faAngleRight} />
                ) : (
                  <FontAwesomeIcon icon={faAngleDown} />
                )}
              </span>
              Term Plan
            </h4>
            {expandedSection === "termPlan" && (
              <div className="section-content">
                <button onClick={() => handlePopup("PDF link")}>
                  PDF link (pop up view)
                </button>
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
}



/* Add your existing styles here */

.rating-select {
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}

.rating-select label {
  margin-bottom: 5px;
  cursor: pointer;
}

textarea {
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
}
