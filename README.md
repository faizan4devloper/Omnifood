import React, { useState } from "react";
import "./Insights.css";

export function Insights({ selectedSchool }) {
    const [showPopup, setShowPopup] = useState(false);
    const [popupContent, setPopupContent] = useState("");

    const handlePopup = (content) => {
        setPopupContent(content);
        setShowPopup(true);
    };

    const closePopup = () => {
        setShowPopup(false);
        setPopupContent("");
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            {selectedSchool && (
                <div>
                    <h4>Selected School: {selectedSchool}</h4>
                    <div className="section">
                        <h5>Parent Reviews</h5>
                        <p>Overall Rating - one liner</p>
                        <button onClick={() => handlePopup("Review Summary")}>Review Summary (pop up)</button>
                    </div>
                    <div className="section">
                        <h5>Ofsted Rating</h5>
                        <textarea placeholder="Text box"></textarea>
                    </div>
                    <div className="section">
                        <h5>Admission Trend</h5>
                        <p>Admissions</p>
                        <p>Appeals</p>
                    </div>
                    <div className="section">
                        <h5>Term Plan</h5>
                        <button onClick={() => handlePopup("PDF link")}>PDF link (pop up view)</button>
                    </div>
                </div>
            )}
            {showPopup && (
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


.insights-container {
    padding: 20px;
}

.section {
    margin-bottom: 20px;
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
    background: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.popup-content h4 {
    margin-top: 0;
}
