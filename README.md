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
                                                    <li key={schoolIdx} onClick={() => handleSchoolClick(school)}>
                                                        {school}
                                                    </li>
                                                ))}
                                            </ul>
                                        )}
                                    </div>
                                ))}
                            </div>






import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
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
    const [activeSchool, setActiveSchool] = useState(null);

    const toggleExpandDescription = (question, index) => {
        const newExpandedDescriptions = { ...expandedDescriptions };
        newExpandedDescriptions[`${question}-${index}`] = !newExpandedDescriptions[
            `${question}-${index}`
        ];
        setExpandedDescriptions(newExpandedDescriptions);
    };

    const handleSchoolClick = (school) => {
        if (activeSchool === school) {
            setActiveSchool(null);
        } else {
            setActiveSchool(school);
        }
    };

    return (
        <div className="chat-container">
            <h1>Frequently Inquired Topics</h1>
            <div className="most-asked-questions">
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
                        className={`selected-question ${
                            expandedQuestions[question] ? "expanded" : ""
                        }`}
                        onClick={() => toggleExpand(question)}
                    >
                        <div className="question-header">
                            <h4>{question}</h4>
                            <FontAwesomeIcon
                                icon={
                                    expandedQuestions[question]
                                        ? faChevronUp
                                        : faChevronDown
                                }
                                className="toggle-icon"
                            />
                        </div>
                        {expandedQuestions[question] && (
                            <div className="descriptions">
                                {questionDescriptions[question].map((desc, idx) => (
                                    <div
                                        key={idx}
                                        className={`description ${
                                            expandedDescriptions[
                                                `${question}-${idx}`
                                            ]
                                                ? "expanded"
                                                : ""
                                        } ${activeSchool === schoolNames[idx] ? 'active' : ''}`}
                                        onClick={() => toggleExpandDescription(question, idx)}
                                    >
                                        <p>{desc}</p>
                                        {expandedDescriptions[
                                            `${question}-${idx}`
                                        ] && (
                                            <ul>
                                                {schoolNames.map((school, schoolIdx) => (
                                                    <li
                                                        key={schoolIdx}
                                                        onClick={() =>
                                                            handleSchoolClick(
                                                                school
                                                            )
                                                        }
                                                    >
                                                        {school}
                                                    </li>
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

export default Chat;
