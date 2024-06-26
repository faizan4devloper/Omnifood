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
    const [expandedQuestions, setExpandedQuestions] = useState({});
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

    const toggleExpand = (question) => {
        setExpandedQuestions((prevExpanded) => ({
            ...prevExpanded,
            [question]: !prevExpanded[question],
        }));
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
                        className={`selected-question ${expandedQuestions[selectedQuestion] ? 'expanded' : ''}`}
                        aria-expanded={expandedQuestions[selectedQuestion]}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestions[selectedQuestion] ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpand(selectedQuestion)}
                            />
                        </div>
                        {expandedQuestions[selectedQuestion] && (
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
                        )}
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
    const [expandedQuestions, setExpandedQuestions] = useState({});
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

    const toggleExpand = (question) => {
        setExpandedQuestions((prevExpanded) => ({
            ...prevExpanded,
            [question]: !prevExpanded[question],
        }));
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
                        className={`selected-question ${expandedQuestions[selectedQuestion] ? 'expanded' : ''}`}
                        aria-expanded={expandedQuestions[selectedQuestion]}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestions[selectedQuestion] ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpand(selectedQuestion)}
                            />
                        </div>
                        {expandedQuestions[selectedQuestion] && (
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
                        )}
                    </div>
                )}
            </div>
        </div>
    );
}







{
  "mostAskedQuestions": [
    "School Transfers",
    "School Placements",
    "Teaching Methodology",
    "SEN/Disability",
    "Enrichment & Extra Curr.",
    "Transportation"
  ],
  "questionDescriptions": {
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
  },
  "schoolNames": ["Cayley", "Mayflower", "Virginia"]
}






import React, { useState, useEffect } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolClick }) {
    const [data, setData] = useState(null);
    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestion, setSelectedQuestion] = useState(null);
    const [expandedQuestions, setExpandedQuestions] = useState({});
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    useEffect(() => {
        fetch('/data.json')
            .then(response => response.json())
            .then(data => setData(data))
            .catch(error => console.error('Error fetching data:', error));
    }, []);

    if (!data) {
        return <div>Loading...</div>;
    }

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

    const toggleExpand = (question) => {
        setExpandedQuestions((prevExpanded) => ({
            ...prevExpanded,
            [question]: !prevExpanded[question],
        }));
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
                    {data.mostAskedQuestions.map((question, index) => (
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
                        className={`selected-question ${expandedQuestions[selectedQuestion] ? 'expanded' : ''}`}
                        aria-expanded={expandedQuestions[selectedQuestion]}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestions[selectedQuestion] ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpand(selectedQuestion)}
                            />
                        </div>
                        {expandedQuestions[selectedQuestion] && (
                            <div className="descriptions active">
                                {data.questionDescriptions[selectedQuestion].map((desc, idx) => (
                                    <div
                                        key={idx}
                                        className={`description ${expandedDescriptions[`${selectedQuestion}-${idx}`] ? 'expanded' : ''}`}
                                        onClick={() => toggleExpandDescription(selectedQuestion, idx)}
                                    >
                                        <p>{desc}</p>
                                        {expandedDescriptions[`${selectedQuestion}-${idx}`] && (
                                            <ul>
                                                {data.schoolNames.map((school, schoolIdx) => (
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
                )}
            </div>
        </div>
    );
}





Here's a brief explanation of how to set up and use `data.json` for your React component:

1. **Create `data.json`**:
   - **Create** a `data.json` file in the `public` directory of your React project. This directory is for static files that will be directly served by the web server.
   - **Add Data**: Populate `data.json` with the structured data you want to use in your component.

2. **Move `data.json` to the `public` Directory**:
   - **Path**: Ensure `data.json` is placed in `public/data.json`.

3. **Fetch Data in the Component**:
   - **Import Necessary Hooks**: Use `useState` and `useEffect` from React.
   - **Fetch JSON**: In the `useEffect` hook, fetch the `data.json` file from `/data.json` (relative URL for static files in the `public` directory).
   - **Set Data**: Store the fetched data in the component's state using `useState`.

4. **Render Data**:
   - **Conditional Rendering**: Check if the data is loaded before rendering the component to avoid errors.
   - **Use Data**: Map over the fetched data to display the questions and descriptions dynamically.

By following these steps, you decouple your data from your component, making it easier to manage and update without changing the component's code.






Sure, here's an explanation of how the code accesses `data.json`:

### 1. Place `data.json` in the `public` Directory
First, ensure `data.json` is in the `public` directory of your React project. The `public` directory is where you put static files that will be served directly.

```
my-react-app/
├── public/
│   ├── data.json
│   └── index.html
├── src/
│   ├── components/
│   │   └── Chat.js
│   ├── App.js
│   ├── index.js
└── ...
```

### 2. Fetch `data.json` in Your Component
In your `Chat.js` component, use `fetch` to get the data from `data.json` and store it in the component's state.

```jsx
import React, { useState, useEffect } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolClick }) {
    const [data, setData] = useState(null);  // State to hold the fetched data
    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestion, setSelectedQuestion] = useState(null);
    const [expandedQuestions, setExpandedQuestions] = useState({});
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    // Fetch the data from data.json
    useEffect(() => {
        fetch('/data.json')  // Fetch data.json from the public directory
            .then(response => response.json())  // Parse the JSON response
            .then(data => setData(data))  // Store the data in the component's state
            .catch(error => console.error('Error fetching data:', error));
    }, []);  // Empty dependency array ensures this runs once after the initial render

    if (!data) {
        return <div>Loading...</div>;  // Show a loading message while the data is being fetched
    }

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

    const toggleExpand = (question) => {
        setExpandedQuestions((prevExpanded) => ({
            ...prevExpanded,
            [question]: !prevExpanded[question],
        }));
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
                    {data.mostAskedQuestions.map((question, index) => (
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
                        className={`selected-question ${expandedQuestions[selectedQuestion] ? 'expanded' : ''}`}
                        aria-expanded={expandedQuestions[selectedQuestion]}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestions[selectedQuestion] ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpand(selectedQuestion)}
                            />
                        </div>
                        {expandedQuestions[selectedQuestion] && (
                            <div className="descriptions active">
                                {data.questionDescriptions[selectedQuestion].map((desc, idx) => (
                                    <div
                                        key={idx}
                                        className={`description ${expandedDescriptions[`${selectedQuestion}-${idx}`] ? 'expanded' : ''}`}
                                        onClick={() => toggleExpandDescription(selectedQuestion, idx)}
                                    >
                                        <p>{desc}</p>
                                        {expandedDescriptions[`${selectedQuestion}-${idx}`] && (
                                            <ul>
                                                {data.schoolNames.map((school, schoolIdx) => (
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
                )}
            </div>
        </div>
    );
}
```

### Explanation

1. **State Initialization**:
   - `const [data, setData] = useState(null);`: Initializes a state variable `data` to hold the fetched data.

2. **Fetching Data**:
   - `useEffect(() => { fetch('/data.json')...}, []);`: The `useEffect` hook runs once after the initial render to fetch `data.json` from the `public` directory. The empty dependency array `[]` ensures this effect runs only once.

3. **Handling Fetched Data**:
   - `fetch('/data.json')`: Fetches the `data.json` file.
   - `.then(response => response.json())`: Parses the JSON response.
   - `.then(data => setData(data))`: Updates the `data` state with the parsed JSON data.

4. **Conditional Rendering**:
   - `if (!data) { return <div>Loading...</div>; }`: Shows a loading message while the data is being fetched.

5. **Using the Fetched Data**:
   - `data.mostAskedQuestions.map(...)`: Uses the fetched data to dynamically render the list of questions.
   - `data.questionDescriptions[selectedQuestion].map(...)`: Uses the fetched data to render descriptions for the selected question.
   - `data.schoolNames.map(...)`: Uses the fetched data to render the list of schools for each description.







Sure, here's an explanation of how the code accesses data.json:1. Place data.json in the public DirectoryFirst, ensure data.json is in the public directory of your React project. The public directory is where you put static files that will be served directly.my-react-app/
├── public/
│   ├── data.json
│   └── index.html
├── src/
│   ├── components/
│   │   └── Chat.js
│   ├── App.js
│   ├── index.js
└── ...2. Fetch data.json in Your ComponentIn your Chat.js component, use fetch to get the data from data.json and store it in the component's state.import React, { useState, useEffect } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolClick }) {
    const [data, setData] = useState(null);  // State to hold the fetched data
    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestion, setSelectedQuestion] = useState(null);
    const [expandedQuestions, setExpandedQuestions] = useState({});
    const [expandedDescriptions, setExpandedDescriptions] = useState({});

    // Fetch the data from data.json
    useEffect(() => {
        fetch('/data.json')  // Fetch data.json from the public directory
            .then(response => response.json())  // Parse the JSON response
            .then(data => setData(data))  // Store the data in the component's state
            .catch(error => console.error('Error fetching data:', error));
    }, []);  // Empty dependency array ensures this runs once after the initial render

    if (!data) {
        return <div>Loading...</div>;  // Show a loading message while the data is being fetched
    }

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

    const toggleExpand = (question) => {
        setExpandedQuestions((prevExpanded) => ({
            ...prevExpanded,
            [question]: !prevExpanded[question],
        }));
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
                    {data.mostAskedQuestions.map((question, index) => (
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
                        className={`selected-question ${expandedQuestions[selectedQuestion] ? 'expanded' : ''}`}
                        aria-expanded={expandedQuestions[selectedQuestion]}
                    >
                        <div className="question-header">
                            <h4>{selectedQuestion}</h4>
                            <FontAwesomeIcon
                                icon={expandedQuestions[selectedQuestion] ? faChevronUp : faChevronDown}
                                className="toggle-icon"
                                onClick={() => toggleExpand(selectedQuestion)}
                            />
                        </div>
                        {expandedQuestions[selectedQuestion] && (
                            <div className="descriptions active">
                                {data.questionDescriptions[selectedQuestion].map((desc, idx) => (
                                    <div
                                        key={idx}
                                        className={`description ${expandedDescriptions[`${selectedQuestion}-${idx}`] ? 'expanded' : ''}`}
                                        onClick={() => toggleExpandDescription(selectedQuestion, idx)}
                                    >
                                        <p>{desc}</p>
                                        {expandedDescriptions[`${selectedQuestion}-${idx}`] && (
                                            <ul>
                                                {data.schoolNames.map((school, schoolIdx) => (
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
                )}
            </div>
        </div>
    );
}ExplanationState Initialization:const [data, setData] = useState(null);: Initializes a state variable data to hold the fetched data.Fetching Data:useEffect(() => { fetch('/data.json')...}, []);: The useEffect hook runs once after the initial render to fetch data.json from the public directory. The empty dependency array [] ensures this effect runs only once.Handling Fetched Data:fetch('/data.json'): Fetches the data.json file..then(response => response.json()): Parses the JSON response..then(data => setData(data)): Updates the data state with the parsed JSON data.Conditional Rendering:if (!data) { return <div>Loading...</div>; }: Shows a loading message while the data is being fetched.Using the Fetched Data:data.mostAskedQuestions.map(...): Uses the fetched data to dynamically render the list of questions.data.questionDescriptions[selectedQuestion].map(...): Uses the fetched data to render descriptions for the selected question.data.schoolNames.map(...): Uses the fetched data to render the list of schools for each description.By following this approach, the component fetches data from data.json and uses it dynamically, making it easier to manage and update the data without modifying the component's code.
