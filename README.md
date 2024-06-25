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
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestion(question);
        setExpandedDescriptions({});
        onQuestionClick(question);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    const toggleExpandDescription = (question, index) => {
        setExpandedDescriptions((prevExpanded) => ({
            [question]: prevExpanded[question] === index ? null : index,
        }));
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
                                icon={expandedDescriptions[selectedQuestion] !== null ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpandDescription(selectedQuestion, expandedDescriptions[selectedQuestion])}
                            />
                        </div>
                        <div className="descriptions">
                            {questionDescriptions[selectedQuestion].map((desc, idx) => (
                                <div
                                    key={idx}
                                    className={`description ${expandedDescriptions[selectedQuestion] === idx ? 'expanded' : ''}`}
                                    onClick={() => toggleExpandDescription(selectedQuestion, idx)}
                                >
                                    <p>{desc}</p>
                                    {expandedDescriptions[selectedQuestion] === idx && (
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






.description {
    padding: 8px;
    border-radius: 4px;
    margin: 8px 0;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.description:hover {
    background-color: #ddd;
}

.description p {
    margin: 0;
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
