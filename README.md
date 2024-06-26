import React, { useState } from "react";
import { Chat } from "./Chat";
import { Insights } from "./Insights";

function App() {
    const [selectedSchool, setSelectedSchool] = useState("");

    const handleSchoolClick = (school) => {
        setSelectedSchool(school);
    };

    return (
        <div className="App">
            <Chat onSchoolClick={handleSchoolClick} />
            <Insights selectedSchool={selectedSchool} />
        </div>
    );
}

export default App;



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
           // ... other descriptions
        ],
        // ... other questions
    };

    const schoolNames = ["Cayley", "Mayflower", "Virginia"];

    const [showQuestions, setShowQuestions] = useState(false);
    const [selectedQuestions, setSelectedQuestions] = useState([]);
    const [expandedQuestions, setExpandedQuestions] = useState({});
    const [expandedDescriptions, setExpandedDescriptions] = useState({});
    
    const toggleDescription = (descIndex) => {
        if (expandedDescription === descIndex) {
            setExpandedDescription(null); 
        } else {
            setExpandedDescription(descIndex);
        }
    }

    const handleQuestionClick = (question) => {
        setShowQuestions(false);
        setSelectedQuestions([question, ...selectedQuestions]);
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
        const newExpandedDescriptions = {};
        newExpandedDescriptions[`${question}-${index}`] = !expandedDescriptions[`${question}-${index}`];

        Object.keys(expandedDescriptions).forEach((key) => {
            if (key !== `${question}-${index}`) {
                newExpandedDescriptions[key] = false;
            }
        });

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





import React from "react";
import "./Insights.css";

export function Insights({ selectedSchool }) {
    const renderButtons = () => {
        return (
            <div className="buttons-container">
                <button>Button 1</button>
                <button>Button 2</button>
                <button>Button 3</button>
                <button>Button 4</button>
            </div>
        );
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            {selectedSchool && (
                <div>
                    <h4>Selected School: {selectedSchool}</h4>
                    {renderButtons()}
                </div>
            )}
        </div>
    );
}
