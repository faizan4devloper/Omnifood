import React, { useState, useEffect } from "react";
import Select from "react-select";
import "./Insights.css";

export function Insights({ selectedQuestion, onSendQuestionInfo }) {
  
  const [questionInfo, setQuestionInfo] = useState(null);
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [selectedReview, setSelectedReview] = useState(null);

  // Simulated data for question info
  const questionData = {
    "School Transfers": "Information about School Transfers...",
    "School Placements": "How to appeal a school placement decision.",
    "Teaching Methodology": "Information about Teaching Methodology...",
    "SEN/Disability": "Information about SEN/Disability...",
    "Enrichment & Extra Curr.": "Information about Enrichment & Extra Curricular...",
    "Transportation": "Information about Transportation..."
  };

  const reviewData = [
    { id: 1, name: "John Doe", photo: "path_to_photo1.jpg", review: "Great insights on school transfers!" },
    { id: 2, name: "Jane Smith", photo: "path_to_photo2.jpg", review: "Very helpful information on SEN/Disability." }
  ];

  useEffect(() => {
    // Update question info when selected question changes
    if (selectedQuestion) {
      setQuestionInfo(questionData[selectedQuestion]);
    } else {
      setQuestionInfo(null);
    }
  }, [selectedQuestion]);

  const handleSendQuestionInfo = () => {
    if (questionInfo) {
      onSendQuestionInfo(questionInfo);
    }
  };

  const handleReviewClick = (review) => {
    setSelectedReview(review);
    setIsModalOpen(true);
  };

  const closeModal = () => {
    setIsModalOpen(false);
    setSelectedReview(null);
  };

  return (
    <div className="insights-container">
      <h3>Insights</h3>
      {questionInfo && (
        <div className="selected-question">
          <h4>{selectedQuestion}</h4>
          <p onClick={handleSendQuestionInfo}>{questionInfo}</p>
        </div>
      )}
      <div className="review-section">
        <h4>Reviews</h4>
        {reviewData.map((review) => (
          <div key={review.id} className="review" onClick={() => handleReviewClick(review)}>
            <img src={review.photo} alt={review.name} className="review-photo" />
            <p>{review.name}</p>
          </div>
        ))}
      </div>

      {isModalOpen && selectedReview && (
        <div className="modal">
          <div className="modal-content">
            <span className="close-button" onClick={closeModal}>&times;</span>
            <h4>{selectedReview.name}</h4>
            <p>{selectedReview.review}</p>
          </div>
        </div>
      )}
    </div>
  );
}
