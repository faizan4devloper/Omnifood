import React from "react";
import "./Landing.css";

export function Landing({ onEnterMain }) {
  return (
    <div className="landing">
      <h2 onClick={onEnterMain}>UK Citizen Advisor</h2>
      <div className="cards-container">
        <div className="card">
          <h4>Education Advisor</h4>
          <p>Description about Education Advisor.</p>
          <button onClick={onEnterMain}>
            Learn More
            <span className="arrow-right">&rarr;</span>
          </button>
        </div>
        <div className="card">
          <h4>Job Advisor</h4>
          <p>Description about Job Advisor.</p>
          <button onClick={onEnterMain}>
            Learn More
            <span className="arrow-right">&rarr;</span>
          </button>
        </div>
        <div className="card">
          <h4>Health Advisor</h4>
          <p>Description about Health Advisor.</p>
          <button onClick={onEnterMain}>
            Learn More
            <span className="arrow-right">&rarr;</span>
          </button>
        </div>
      </div>
    </div>
  );
}












/* Landing.css */

.cards-container {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 180px auto;
    margin-bottom: 0;
}

.landing h2 {
    text-align: center;
    cursor: pointer;
    font-size: 2rem;
    margin-bottom: 20px;
    color: #333; /* Color for the heading */
}

.cards-container .card {
    border-radius: 10px;
    width: 300px;
    height: 220px;
    background: rgba(245, 245, 245, 0.9);
    box-shadow: 0 10px 8px rgba(0, 0, 0, 0.2);
    color: #fff;
    margin: 20px;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s ease;
}

.cards-container .card::before {
    content: '';
    position: absolute;
    left: 0;
    bottom: -100%;
    width: 100%;
    height: 100%;
    background: rgba(135, 206, 250, 0.7);
    z-index: 0;
    transition: bottom 0.3s ease;
}

.cards-container .card:hover::before {
    bottom: 0;
}

.cards-container .card:hover {
    transform: scale(1.05);
}

.card h4 {
    position: relative;
    z-index: 1;
    text-align: center;
    color: #1f77f6; /* Color for the heading */
    margin-top: 90px; /* Adjust to center the heading vertically */
    transition: margin-top 0.3s ease; /* Smooth transition for the heading */
}

.card p, .card button {
    position: relative;
    z-index: 1;
    text-align: center;
    color: #ddd; /* Color for the description */
    margin: 10px 20px;
    opacity: 0;
    transform: translateY(10px); /* Slightly move down initially */
    transition: opacity 0.3s ease, transform 0.3s ease; /* Smooth transition for appearance */
}

.cards-container .card:hover h4 {
    margin-top: 20px; /* Move the heading up when hovered */
}

.cards-container .card:hover p,
.cards-container .card:hover button {
    opacity: 1;
    transform: translateY(0); /* Move to original position */
}

.card button {
    border: none;
    background: #1f77f6;
    color: white;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.card button .arrow-right {
    margin-left: 8px;
    transition: margin-left 0.3s ease; /* Smooth transition for arrow */
}

.card button:hover .arrow-right {
    margin-left: 12px; /* Slightly move arrow right on hover */
}
