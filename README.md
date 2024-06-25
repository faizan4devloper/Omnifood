import React, { useState } from "react";
import { ChatScreen } from "./ChatScreen";
import { Chat } from "./Chat";
import { Insights } from "./Insights";
import Modal from "./Modal";

const getLocalityFromPostcode = async (postcode) => {
  // Mock response - replace this with an actual API call
  const postcodeToLocalityMap = {
    "SW1A 1AA": "Westminster",
    "E1 6AN": "Shoreditch",
    "M1 1AE": "Manchester",
    "E14 0HE": "London Borough of Tower Hamlets",
  };

  return postcodeToLocalityMap[postcode] || "Unknown locality";
};

function MainContainer({ advisorType }) {
  const [selectedQuestion, setSelectedQuestion] = useState(null);
  const [isModalOpen, setIsModalOpen] = useState(true);
  const [postcode, setPostcode] = useState("");
  const [locality, setLocality] = useState("");

  const handleQuestionClick = (question) => {
    setSelectedQuestion(question);
  };

  const handleSendQuestionInfo = (questionInfo) => {
    console.log("Question info sent to Chat:", questionInfo);
  };

  const handleCloseModal = () => {
    setIsModalOpen(false);
  };

  const handlePostcodeApply = async (postcode) => {
    const localityName = await getLocalityFromPostcode(postcode);
    setPostcode(postcode);
    setLocality(localityName);
    setIsModalOpen(false);
  };

  return (
    <div className="main-container">
      <h2 className="advisor-heading">
        {advisorType} Advisor {locality && `- ${locality}`}
      </h2>
      <ChatScreen />
      <Chat onQuestionClick={handleQuestionClick} />
      <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
      <Modal isOpen={isModalOpen} onClose={handleCloseModal} onPostcodeApply={handlePostcodeApply}>
        {/* You can pass additional children here if needed */}
      </Modal>
    </div>
  );
}

export default MainContainer;


@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap");

body,
html {
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  margin: 0;
  padding: 0;
  font-family: "Poppins", Arial, sans-serif;
  scroll-behavior: smooth;
  overflow: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
}
body::-webkit-scrollbar {
  width: 0px;
  background: transparent;
  
}
.main-container {
  display: flex;
  justify-content: center;
  
}

.advisor-heading {
  position: absolute;
  right:38%;
  margin:10px;
  text-align: center;
  font-size: 2rem;
  color: #333; 
}

.breadcrumbs {
  position: absolute;
  top:-5px;
  padding: 10px;
}

.breadcrumbs ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.breadcrumbs ul li {
  display: inline;
}

.breadcrumbs ul li:not(:first-child)::before {
  content: ">";
  color:#fff;
  font-size: 20px;
  margin: 0 5px;
}

.breadcrumbs ul li a {
  text-decoration: none;
  color: #fff;
  font-weight: bold;
  font-size: 16px;
  padding: 5px;
}

.breadcrumbs ul li a:hover {
  color: #ccc; 
}

.breadcrumbs ul li span {
  color: #777;
  padding: 5px;
}

.breadcrumbs ul li.active a {
  color:red;
  text-decoration: underline;
}

.breadcrumbs ul li.active a:hover {
  color: #1559b3;
}
