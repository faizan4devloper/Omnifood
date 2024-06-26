import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolClick }) {
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
        // ... other questions
    };

    const schoolNames = ["Cayley", "Mayflower", "Virginia"];

    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestions, setSelectedQuestions] = useState([]);
    const [expandedQuestion, setExpandedQuestion] = useState(null);
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestions([question, ...selectedQuestions.filter(q => q !== question)]);
        onQuestionClick(question);
    };

    const handleSchoolClick = (school) => {
        onSchoolClick(school);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    const toggleExpand = (question) => {
        setExpandedQuestion(expandedQuestion === question ? null : question);
    };

    const toggleExpandDescription = (question, index) => {
        const newExpandedDescriptions = {};

        // Collapse all other descriptions under the same question
        for (let i = 0; i < questionDescriptions[question].length; i++) {
            newExpandedDescriptions[`${question}-${i}`] = i === index;
        }

        setExpandedDescriptions(newExpandedDescriptions);
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
                        className={`selected-question ${expandedQuestion === question ? 'expanded' : ''}`}
                        aria-expanded={expandedQuestion === question}
                    >
                        <div className="question-header">
                            <h4>{question}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestion === question ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpand(question)}
                            />
                        </div>
                        {expandedQuestion === question && (
                            <div className="descriptions active">
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
                        )}
                    </div>
                ))}
            </div>
        </div>
    );
}





import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolClick }) {
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
        // ... other questions
    };

    const schoolNames = ["Cayley", "Mayflower", "Virginia"];

    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestion, setSelectedQuestion] = useState(null);
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestion(question);
        onQuestionClick(question);
    };

    const handleSchoolClick = (school) => {
        onSchoolClick(school);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    const toggleExpandDescription = (question, index) => {
        const newExpandedDescriptions = {};

        // Collapse all other descriptions under the same question
        for (let i = 0; i < questionDescriptions[question].length; i++) {
            newExpandedDescriptions[`${question}-${i}`] = i === index;
        }

        setExpandedDescriptions(newExpandedDescriptions);
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
                    <div
                        key={selectedQuestion}
                        className="selected-question expanded"
                        aria-expanded={true}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                        </div>
                        <div className="descriptions active">
                            {questionDescriptions[selectedQuestion].map((desc, idx) => (
                                <div
                                    key={idx}
                                    className={`description ${expandedDescriptions[`${selectedQuestion}-${idx}`] ? 'expanded' : ''}`}
                                    onClick={() => toggleExpandDescription(selectedQuestion, idx)}
                                >
                                    <p>{desc}</p>
                                    {expandedDescriptions[`${selectedQuestion}-${idx}`] && (
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
                    </div>
                )}
            </div>
        </div>
    );
}




import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolClick }) {
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
        // ... other questions
    };

    const schoolNames = ["Cayley", "Mayflower", "Virginia"];

    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestion, setSelectedQuestion] = useState(null);
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestion(question === selectedQuestion ? null : question);
        onQuestionClick(question);
    };

    const handleSchoolClick = (school) => {
        onSchoolClick(school);
    };

    const toggleQuestions = () => {
        setShowQuestions(!showQuestions);
    };

    const toggleExpandDescription = (question, index) => {
        setExpandedDescriptions((prevExpandedDescriptions) => ({
            ...prevExpandedDescriptions,
            [`${question}-${index}`]: !prevExpandedDescriptions[`${question}-${index}`]
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
                    <div
                        key={selectedQuestion}
                        className="selected-question expanded"
                        aria-expanded={true}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={faChevronUp}
                                className="toggle-icon"
                                onClick={() => setSelectedQuestion(null)}
                            />
                        </div>
                        <div className="descriptions active">
                            {questionDescriptions[selectedQuestion].map((desc, idx) => (
                                <div
                                    key={idx}
                                    className={`description ${expandedDescriptions[`${selectedQuestion}-${idx}`] ? 'expanded' : ''}`}
                                    onClick={() => toggleExpandDescription(selectedQuestion, idx)}
                                >
                                    <p>{desc}</p>
                                    {expandedDescriptions[`${selectedQuestion}-${idx}`] && (
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
                    </div>
                )}
            </div>
        </div>
    );
}
