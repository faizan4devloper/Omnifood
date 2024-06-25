import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick }) {
    const mostAskedQuestions = [
        "School Transfers",
        "School Placements",
        "Teaching Methodology",
        "SEN/Disability",
        "Enrichment & Extra Curr.",
        "Transportation"
    ];

    const questionDescriptions = {
        "School Transfers": [
            "Description 1 for School Transfers",
            "Description 2 for School Transfers",
            "Description 3 for School Transfers",
            "Description 4 for School Transfers",
            "Description 5 for School Transfers"
        ],
        "School Placements": [
            "Description 1 for School Placements",
            "Description 2 for School Placements",
            "Description 3 for School Placements",
            "Description 4 for School Placements",
            "Description 5 for School Placements"
        ],
        "Teaching Methodology": [
            "Description 1 for Teaching Methodology",
            "Description 2 for Teaching Methodology",
            "Description 3 for Teaching Methodology",
            "Description 4 for Teaching Methodology",
            "Description 5 for Teaching Methodology"
        ],
        "SEN/Disability": [
            "Description 1 for SEN/Disability",
            "Description 2 for SEN/Disability",
            "Description 3 for SEN/Disability",
            "Description 4 for SEN/Disability",
            "Description 5 for SEN/Disability"
        ],
        "Enrichment & Extra Curr.": [
            "Description 1 for Enrichment & Extra Curr.",
            "Description 2 for Enrichment & Extra Curr.",
            "Description 3 for Enrichment & Extra Curr.",
            "Description 4 for Enrichment & Extra Curr.",
            "Description 5 for Enrichment & Extra Curr."
        ],
        "Transportation": [
            "Description 1 for Transportation",
            "Description 2 for Transportation",
            "Description 3 for Transportation",
            "Description 4 for Transportation",
            "Description 5 for Transportation"
        ]
    };

    const schoolNames = ["Cayley", "Mayflower", "Virginia"];

    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestion, setSelectedQuestion] = useState(null);
    const [expandedDescription, setExpandedDescription] = useState(null);

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestion(question);
        setExpandedDescription(null);
        onQuestionClick(question);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    const toggleExpandDescription = (index) => {
        setExpandedDescription(expandedDescription === index ? null : index);
    };

    return (
        <div className="chat-container">
            <h1>Frequently Inquired Topics</h1>
            <div className="hamburger-menu" onClick={toggleQuestions}>
                <FontAwesomeIcon icon={showQuestions ? faTimes : faBars} />
            </div>
            <div className={`most-asked-questions ${showQuestions ? 'show' : ''}`}>
                <h4>Frequently Inquired Topics</h4>
                <ul>
                    {mostAskedQuestions.map((question, index) => (
                        <li key={index} onClick={() => handleQuestionClick(question)}>
                            {question}
                        </li>
                    ))}
                </ul>
            </div>
            <div className="selected-questions">
                {selectedQuestion && (
                    <div className="selected-question">
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={expandedDescription !== null ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpandDescription(expandedDescription)}
                            />
                        </div>
                        <div className="descriptions">
                            {questionDescriptions[selectedQuestion].map((desc, idx) => (
                                <div
                                    key={idx}
                                    className={`description ${expandedDescription === idx ? 'expanded' : ''}`}
                                    onClick={() => toggleExpandDescription(idx)}
                                >
                                    <p>{desc}</p>
                                    {expandedDescription === idx && (
                                        <ul>
                                            {schoolNames.map((school, schoolIdx) => (
                                                <li key={schoolIdx}>{school}</li>
                                            ))}
                                        </ul>
                                    )}
                                </div>
                            ))}
                        </div>
                    </div>
                )}
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
    overflow: hidden;
}

.chat-container h1 {
    text-align: left;
    margin-left: 42px;
    margin-top: 12px;
    font-size: 22px;
    color: #fff;
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
    font-size: 14px;
    font-weight: 500;
    margin: 5px 0;
    background-color: #fff;
    color: #000;
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
    margin-top: 30px;
    overflow-y: auto;
    padding: 10px;
    flex-grow: 1;
}

.selected-questions::-webkit-scrollbar {
    width: 8px;
}

.selected-questions::-webkit-scrollbar-thumb {
    background-color: rgba(111, 54, 205, 0.8);
    border-radius: 10px;
}

.selected-questions::-webkit-scrollbar-thumb:hover {
    background-color: rgba(111, 54, 205, 1);
}

.selected-questions::-webkit-scrollbar-track {
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
}

.selected-question {
    background-color: #fff;
    padding: 10px;
    border-radius: 4px;
    margin-bottom: 10px;
    box-shadow: 0 10px 8px rgba(0, 0, 0, 0.2);
    color: #000;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.selected-question h4 {
    margin: 0;
}

.selected-question .question-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.selected-question .toggle-icon {
    font-size: 18px;
}

.selected-question p {
    margin: 10px 0 0;
    display: none;
    animation: fadeIn 0.3s ease-in-out forwards;
}

.selected-question.expanded p {
    font-size: 14px;
    display: block;
    transition: 0.1s ease-in;
}

.description {
    padding: 8px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.description:hover {
    background-color: #ddd;
}

.description.expanded ul {
    display: block;
}

.description ul {
    list-style: none;
    padding: 0;
    margin: 10px 0 0;
    display: none;
    animation: fadeIn 0.3s ease-in-out forwards;
}

.description ul li {
    background-color: #e0e0e0;
    padding: 5px;
    color: #000;
    border-radius: 4px;
    margin: 5px 0;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
