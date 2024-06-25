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







.review-section {
  margin-top: 20px;
  text-align: center;
}

.review {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  cursor: pointer;
}

.review-photo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  max-width: 500px;
  border-radius: 10px;
  animation: fadeIn 0.5s ease-in-out;
}

.close-button {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close-button:hover,
.close-button:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
