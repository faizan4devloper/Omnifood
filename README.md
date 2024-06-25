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
