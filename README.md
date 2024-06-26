import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faAngleRight, faAngleDown } from "@fortawesome/free-solid-svg-icons";
import "./Insights.css";
import ParentReview from "./ParentReview";

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

  const handlePopup = () => {
    setPopupContent("parentReviews");
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
                <button onClick={handlePopup}>Review Summary (pop up)</button>
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
                <textarea
                  placeholder="Enter Ofsted Rating here..."
                  rows={5}
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
      {popupContent === "parentReviews" && (
        <ParentReview closePopup={closePopup} />
      )}
    </div>
  );
};

export default Insights;



import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faAngleRight, faAngleDown } from "@fortawesome/free-solid-svg-icons";
import "./Insights.css";
import ParentReview from "./ParentReview";

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

  const handlePopup = () => {
    setPopupContent("parentReviews");
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
                <button onClick={handlePopup}>Review Summary (pop up)</button>
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
                <textarea
                  placeholder="Enter Ofsted Rating here..."
                  rows={5}
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
      {popupContent === "parentReviews" && (
        <ParentReview closePopup={closePopup} />
      )}
    </div>
  );
};

export default Insights;
