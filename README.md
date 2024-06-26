    import React, { useState } from "react";
    import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
    import { faAngleRight, faAngleDown} from "@fortawesome/free-solid-svg-icons";
    import "./Insights.css";
    
    export function Insights  ({ selectedSchool })  {
      const [popupContent, setPopupContent] = useState(null);
      const [expandedSection, setExpandedSection] = useState(null);
    
      const handleExpand = (section) => {
        if (expandedSection === section) {
          setExpandedSection(null);
        } else {
          setExpandedSection(section);
        }   
      };
    
      const handlePopup = (content) => {
        setPopupContent(content);
      };
    
      const closePopup = () => {
        setPopupContent(null);
      };
    
      return (
        <div className="insights-container">
          <h3>Insights : {selectedSchool}</h3>
          {selectedSchool && (
            <div>
              <div className="section">
                <h4 onClick={() => handleExpand("parentReviews")}>
                  <span className="expand-icon">{expandedSection === "parentReviews" ? <FontAwesomeIcon icon={faAngleRight} /> : <FontAwesomeIcon icon={faAngleDown} />}</span>
                  Parent Reviews
                </h4>
                {expandedSection === "parentReviews" && (
                  <div className="section-content">
                    <p>Overall Rating - one liner</p>
                    <button onClick={() => handlePopup("Review Summary")}>Review Summary (pop up)</button>
                  </div>
                )}
              </div>
              <div className="section">
                <h4 onClick={() => handleExpand("ofstedRating")}>
                  <span className="expand-icon">{expandedSection === "ofstedRating" ? <FontAwesomeIcon icon={faAngleRight} /> : <FontAwesomeIcon icon={faAngleDown} />}</span>
                  Ofsted Rating
                </h4>
                {expandedSection === "ofstedRating" && (
                  <div className="section-content">
                    <textarea placeholder="Enter Ofsted Rating here..." rows={5}></textarea>
                  </div>
                )}
              </div>
              <div className="section">
                <h4 onClick={() => handleExpand("admissionTrend")}>
                  <span className="expand-icon">{expandedSection === "admissionTrend" ? <FontAwesomeIcon icon={faAngleRight} /> : <FontAwesomeIcon icon={faAngleDown} />}</span>
                  Admission Trend
                </h4>
                {expandedSection === "admissionTrend" && (
                  <div className="section-content">
                    <p>Admissions: Enter admissions details here...</p>
                    <p>Appeals: Enter appeals details here...</p>
                  </div>
                )}
              </div>
              <div className="section">
                <h4 onClick={() => handleExpand("termPlan")}>
                  <span className="expand-icon">{expandedSection === "termPlan" ? <FontAwesomeIcon icon={faAngleRight} /> : <FontAwesomeIcon icon={faAngleDown} />}</span>
                  Term Plan
                </h4>
                {expandedSection === "termPlan" && (
                  <div className="section-content">
                    <button onClick={() => handlePopup("PDF link")}>PDF link (pop up view)</button>
                  </div>
                )}
              </div>
            </div>
          )}
          {popupContent && (
            <div className="popup">
              <div className="popup-content">
                <h4>Strengths:
- Excellent academic standards and results: Many parents praise the school's strong focus on academics and the high-quality education their children receive.
- Inclusive and diverse environment: Parents appreciate the school's diverse student population and inclusive, welcoming atmosphere.
- Dedicated and supportive staff: Teachers and the leadership team are often described as caring, approachable, and committed to the students' well-being.
- Extracurricular activities: The school offers a wide range of after-school clubs and activities, providing opportunities for students to explore their interests.
- Communication and parental engagement: Parents feel well-informed about their child's progress and appreciate the school's efforts to involve families in the learning process.
 
Areas for Improvement:
- Facility maintenance: A few parents have expressed concerns about the upkeep and cleanliness of the school premises, particularly the outdoor areas.
- Lunch options: Some parents would like to see more varied and healthier lunch options for students.
- Class sizes: A small number of parents have raised concerns about larger class sizes, which they feel can impact individual attention and support.
 
Parental Testimonials:
"Cayley Primary is an excellent school. The teachers are highly committed, and the academic standards are outstanding. My child has thrived here."
"The diversity of the school community is wonderful, and my child has made great friends from different backgrounds. The atmosphere is inclusive and welcoming."
"The school leadership is very responsive to parental feedback, and they work hard to address any concerns. I'm pleased with the overall experience."
"While the facilities could use some upgrades, the education my child receives at Cayley is top-notch. The teachers go above and beyond to support the students."
 
Overall, Cayley Primary School in Tower Hamlets appears to be a well-regarded primary school, with a strong focus on academics, a diverse and inclusive environment, and dedicated staff. Parents generally express satisfaction with the quality of education and the school's commitment to their children's well-being.</h4>
                <button onClick={closePopup}>Close</button>
              </div>
            </div>
          )}
        </div>
      );
    };
    
