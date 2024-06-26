import React, { useState } from "react";
import "./Insights.css";

export function Insights() {
    const [isModalOpen, setIsModalOpen] = useState(false);
    const [selectedReview, setSelectedReview] = useState(null);

    const reviewData = [
        { id: 1, name: "John Doe", photo: "path_to_photo1.jpg", review: "Great insights on school transfers!" },
        { id: 2, name: "Jane Smith", photo: "path_to_photo2.jpg", review: "Very helpful information on SEN/Disability." }
    ];

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


.insights-container {
    background-color: rgba(0, 0, 0, 0.5);
    margin: 80px 0 0 10px;
    border-radius: 10px;
    width: 400px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease-in-out;
}

/*.insights-container:hover {*/
/*    transform: scale(1.02);*/
/*}*/

.insights-container h3 {
    text-align: center;
    color: #fff;
}

.locality-section {
    margin-top: 20px;
    text-align: center;
}

.locality-section h4 {
    color: #fff;
    margin-bottom: 10px;
}

.dropdown {
    width: 100%;
    margin-bottom: 20px;
}

.selected-message {
    margin-top: 15px;
    color: #fff;
    font-size: 1.2em;
    animation: fadeIn 0.5s ease-in-out;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

/* Custom styles for react-select */
.react-select__control {
    background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    color: white;
    border: none;
    border-radius: 5px;
    box-shadow: none;
}

.react-select__menu {
    background-color: white;
    border-radius: 5px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.react-select__option--is-focused {
    background-color: #f1f1f1;
}

.react-select__option--is-selected {
    background-color: #1f77f6;
    color: white;
}

.selected-question{
  margin-top: 20px;
  background-color: rgba(255, 255, 255, 0.1);
  padding: 10px;
  border-radius: 5px;
  color:#fff;
  animation:fadeIn 0.5 ease-in-out;
}

.selected-question h4{
  margin-bottom: 10px;
}


.review-section {
  margin-top: 20px;
  text-align: center;
}

.review {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 10px;
  cursor: pointer;
  background-color: #fff;
  border-radius: 10px;
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
