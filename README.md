import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick }) {
    const [mostAskedQuestions] = useState([
        "School Transfers",
        "School Placements",
        "Teaching Methodology",
        "SEN/Disability",
        "Enrichment & Extra Curr.",
        "Transportation"
    ]);
    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestions, setSelectedQuestions] = useState([]);

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestions([question, ...selectedQuestions]);
        onQuestionClick(question);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    return (
        <div className="chat-container">
            <div className="hamburger-menu" onClick={toggleQuestions}>
                <FontAwesomeIcon icon={showQuestions ? faTimes : faBars} />
            </div>
            <div className={`most-asked-questions ${showQuestions ? 'show' : ''}`}>
                <h4>Most Asked Questions</h4>
                <ul>
                    {mostAskedQuestions.map((question, index) => (
                        <li key={index} onClick={() => handleQuestionClick(question)}>
                            {question}
                        </li>
                    ))}
                </ul>
            </div>
            <div className="selected-questions">
                {selectedQuestions.map((question, index) => (
                    <div key={index} className="selected-question">
                        <p>{question}</p>
                    </div>
                ))}
            </div>
        </div>
    );
}






.chat-container {
    background-color: rgba(0, 0, 0, 0.5);
    margin: 80px 0 0 10px;
    border-radius: 10px;
    width: 450px;
    display: flex;
    flex-direction: column;
    height: 500px;
    position: relative;
    overflow: hidden; /* Ensure the animated elements stay within bounds */
}

.hamburger-menu {
    position: absolute;
    top: 10px;
    left: 10px;
    font-size: 24px;
    color: #fff;
    cursor: pointer;
    z-index: 10;
}

.most-asked-questions {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    display: flex;
    border-radius: 10px;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 5;
    color: white;
    transform: translateY(-100%);
    transition: transform 0.3s ease-in-out;
}

.most-asked-questions.show {
    transform: translateY(0);
}

.most-asked-questions h4 {
    margin-bottom: 20px;
    opacity: 0;
    animation: fadeIn 0.5s 0.2s forwards;
}

.most-asked-questions ul {
    list-style: none;
    padding: 0;
    opacity: 0;
    animation: fadeIn 0.5s 0.4s forwards;
}

.most-asked-questions li {
    padding: 10px 20px;
    font-size:14px;
    font-weight:500;
    margin: 5px 0px;
    background-color: #fff;
    color:#000;
    border-radius: 4px;
    cursor: pointer;
    box-shadow: 0 10px 8px rgba(0, 0, 0, 0.2);
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.most-asked-questions li:hover {
    background-color: rgba(0, 0, 0, 0.5);
    color: #fff;
    transform: scale(1.05);
}

.selected-questions {
    margin-top: 80px;
    overflow-y: auto;
    padding: 10px;
    flex-grow: 1;
}

.selected-question {
    background-color: #fff;
    padding: 10px;
    border-radius: 4px;
    margin-bottom: 10px;
    box-shadow: 0 10px 8px rgba(0, 0, 0, 0.2);
    color: #000;
}

.selected-question p {
    margin: 0;
}
