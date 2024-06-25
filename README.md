import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes, faChevronDown, faChevronUp } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick, onSchoolSelect }) {
    const mostAskedQuestions = [
        "School Transfers",
        "School Placements",
        "Teaching Methodology",
        "SEN/Disability",
        "Enrichment & Extra Curr.",
        "Transportation"
    ];

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
        const newExpandedDescriptions = {};

        newExpandedDescriptions[`${question}-${index}`] = !expandedDescriptions[`${question}-${index}`];

        Object.keys(expandedDescriptions).forEach((key) => {
            if (key !== `${question}-${index}`) {
                newExpandedDescriptions[key] = false;
            }
        });

        setExpandedDescriptions(newExpandedDescriptions);
    };

    const handleSchoolSelect = (schoolName) => {
        // Simulate fetching data for the selected school
        const schoolInfo = {
            schoolName,
            parentReview: "Excellent parent reviews",
            ofstedRatings: "Outstanding",
            admissionTrends: "Increasing admissions",
            termPlan: "Focus on holistic development"
        };
        
        // Pass schoolInfo to parent component (App.js)
        onSchoolSelect(schoolInfo);
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
                                {Array.from({ length: 5 }).map((_, idx) => (
                                    <div
                                        key={idx}
                                        className={`description ${expandedDescriptions[`${question}-${idx}`] ? 'expanded' : ''}`}
                                        onClick={() => toggleExpandDescription(question, idx)}
                                    >
                                        <p>Description {idx + 1}</p>
                                        {expandedDescriptions[`${question}-${idx}`] && (
                                            <ul>
                                                {schoolNames.map((school, schoolIdx) => (
                                                    <li key={schoolIdx} onClick={() => handleSchoolSelect(school)}>{school}</li>
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
import { Login } from "./components/Login/Login";
import { Landing } from "./components/Landing/Landing";
import MainContainer from "./components/main/MainContainer";
import { Insights } from "./components/Insights/Insights"; // Import Insights component
import "./App.css";

function App() {
    const [view, setView] = useState("login");
    const [advisorType, setAdvisorType] = useState("");
    const [selectedSchool, setSelectedSchool] = useState(null); // State to store selected school info

    const handleLogin = () => {
        setView("landing");
    };

    const handleEnterMain = (type) => {
        setAdvisorType(type);
        setView("main");
    };

    const handleGoBack = () => {
        if (view === "landing") {
            setView("login");
        } else if (view === "main") {
            setView("landing");
        }
    };

    const handleSchoolSelect = (schoolInfo) => {
        setSelectedSchool(schoolInfo);
    };

    return (
        <div className="app">
            <nav className="breadcrumbs">
                <ul>
                    <li>
                        <a href="#" onClick={handleGoBack}>
                            Login
                        </a>
                    </li>
                    {view === "main" && (
                        <>
                            <li>
                                <a href="#">{advisorType} Advisor</a>
                            </li>
                        </>
                    )}
                    {view === "landing" && (
                        <li>
                            <a>Landing</a>
                        </li>
                    )}
                </ul>
            </nav>
            {view === "login" && <Login onLogin={handleLogin} />}
            {view === "landing" && <Landing onEnterMain={handleEnterMain} />}
            {view === "main" && (
                <>
                    <Chat onQuestionClick={() => {}} onSchoolSelect={handleSchoolSelect} />
                    {selectedSchool && <Insights schoolInfo={selectedSchool} />}
                </>
            )}
            {/* Add Insights component with selectedSchool info */}
        </div>
    );
}

export default App;





import React from "react";
import "./Insights.css";

export function Insights({ schoolInfo }) {
    return (
        <div className="insights-container">
            <h3>Insights</h3>
            <div className="selected-message">
                {schoolInfo && (
                    <>
                        <h4>{schoolInfo.schoolName}</h4>
                        <p>Parent Review: {schoolInfo.parentReview}</p>
                        <p>Ofsted Ratings: {schoolInfo.ofstedRatings}</p>
                        <p>Admission Trends: {schoolInfo.admissionTrends}</p>
                        <p>Term Plan: {schoolInfo.termPlan}</p>
                    </>
                )}
            </div>
        </div>
    );
}
