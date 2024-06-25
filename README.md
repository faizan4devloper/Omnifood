// Question.js
import React, { useState } from "react";
import Description from "./Description";

const Question = ({ question, descriptions, onQuestionClick }) => {
  const [expanded, setExpanded] = useState(false);

  const handleQuestionClick = () => {
    setExpanded(!expanded);
    onQuestionClick(question);
  };

  return (
    <div className={`question ${expanded ? "expanded" : ""}`}>
      <h4 onClick={handleQuestionClick}>{question}</h4>
      {expanded && (
        <div className="descriptions">
          {descriptions.map((description, index) => (
            <Description key={index} description={description} />
          ))}
        </div>
      )}
    </div>
  );
};

export default Question;


// Description.js
import React, { useState } from "react";

const Description = ({ description }) => {
  const [expanded, setExpanded] = useState(false);

  const handleDescriptionClick = () => {
    setExpanded(!expanded);
  };

  return (
    <div
      className={`description ${expanded ? "expanded" : ""}`}
      onClick={handleDescriptionClick}
    >
      <p>{description}</p>
    </div>
  );
};

export default Description;


import React from "react";
import Question from "./Question";

const Chat = ({ onQuestionClick }) => {
  // Your data for questions and descriptions
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
      // Descriptions for "School Placements" question
    ],
    // Descriptions for other questions...
  };

  return (
    <div className="chat-container">
      {/* Render questions using Question component */}
      {mostAskedQuestions.map((question, index) => (
        <Question
          key={index}
          question={question}
          descriptions={questionDescriptions[question]}
          onQuestionClick={onQuestionClick}
        />
      ))}
    </div>
  );
};

export default Chat;
