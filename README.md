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
            "Can you help me with Local Authority school in this region along with Parent rating?",
            "What are the admission criteria for the schools in this area? How do they prioritize applications?",
            "What are the average class sizes and student-teacher ratios in the local schools?",
            "What is the academic performance of the schools in this area, as measured by exam results, Ofsted ratings, and other relevant metrics?",
            "What extracurricular activities and clubs are available at the local schools? Are there any specialized programs or facilities?"
        ],
        "School Placements": [
            "Can you help me with Local Authority school in this region along with Parent rating?",
            "What are the admission criteria for the schools in this area? How do they prioritize applications?",
            "What are the average class sizes and student-teacher ratios in the local schools?",
            "What is the academic performance of the schools in this area, as measured by exam results, Ofsted ratings, and other relevant metrics?",
            "What extracurricular activities and clubs are available at the local schools? Are there any specialized programs or facilities?"
        ],
        "Teaching Methodology": [
            "Can you help me with Local Authority school in this region along with Parent rating?",
            "What are the admission criteria for the schools in this area? How do they prioritize applications?",
            "What are the average class sizes and student-teacher ratios in the local schools?",
            "What is the academic performance of the schools in this area, as measured by exam results, Ofsted ratings, and other relevant metrics?",
            "What extracurricular activities and clubs are available at the local schools? Are there any specialized programs or facilities?"
        ],
        "SEN/Disability": [
            "Can you help me with Local Authority school in this region along with Parent rating?",
            "What are the admission criteria for the schools in this area? How do they prioritize applications?",
            "What are the average class sizes and student-teacher ratios in the local schools?",
            "What is the academic performance of the schools in this area, as measured by exam results, Ofsted ratings, and other relevant metrics?",
            "What extracurricular activities and clubs are available at the local schools? Are there any specialized programs or facilities?"
        ],
        "Enrichment & Extra Curr.": [
            "Can you help me with Local Authority school in this region along with Parent rating?",
            "What are the admission criteria for the schools in this area? How do they prioritize applications?",
            "What are the average class sizes and student-teacher ratios in the local schools?",
            "What is the academic performance of the schools in this area, as measured by exam results, Ofsted ratings, and other relevant metrics?",
            "What extracurricular activities and clubs are available at the local schools? Are there any specialized programs or facilities?"
        ],
        "Transportation": [
            "Can you help me with Local Authority school in this region along with Parent rating?",
            "What are the admission criteria for the schools in this area? How do they prioritize applications?",
            "What are the average class sizes and student-teacher ratios in the local schools?",
            "What is the academic performance of the schools in this area, as measured by exam results, Ofsted ratings, and other relevant metrics?",
            "What extracurricular activities and clubs are available at the local schools? Are there any specialized programs or facilities?"
        ]
    };

    const schoolNames = ["Cayley", "Mayflower", "Virginia"];

    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestions, setSelectedQuestions] = useState([]);
    const [expandedQuestions, setExpandedQuestions] = useState({});
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestions([question, ...selectedQuestions]);
        onQuestionClick(question);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    const toggleExpand = (question) => {
        setExpandedQuestions((prevExpanded) => ({
            ...prevExpanded,
            [question]: !prevExpanded[question],
        }));
    };

    const toggleExpandDescription = (question, index) => {
        setExpandedDescriptions({
            [`${question}-${index}`]: !expandedDescriptions[`${question}-${index}`],
        });
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
                {selectedQuestions.map((question, index) => (
                    <div
                        key={index}
                        className={`selected-question ${expandedQuestions[question] ? 'expanded' : ''}`}
                        onClick={() => toggleExpand(question)}
                        aria-expanded={expandedQuestions[question]}
                    >
                        <div className="question-header">
                            <h4>{question}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestions[question] ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                            />
                        </div>
                        {expandedQuestions[question] && (
                            <div className="descriptions">
                                {questionDescriptions[question].map((desc, idx) => (
                                    <div
                                        key={idx}
                                        className={`description ${expandedDescriptions[`${question}-${idx}`] ? 'expanded' : ''}`}
                                        onClick={() => toggleExpandDescription(question, idx)}
                                    >
                                        <p>{desc}</p>
                                        {expandedDescriptions[`${question}-${idx}`] && (
                                            <ul>
                                                {schoolNames.map((school, schoolIdx) => (
                                                    <li key={schoolIdx}>{school}</li>
                                                ))}
                                            </ul>
                                        )}
                                    </div>
                                ))}
                            </div>
                        )}
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
    margin-top: 80px;
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

.selected-question.expanded .descriptions {
    display: block;
}

.descriptions {
    display: none;
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
