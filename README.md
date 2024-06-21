import React from "react";
import "./Landing.css";

export function Landing({onEnterMain}){
    return (
        <div className="landing">
            <h2 onClick={onEnterMain}>UK Citizen Advisor</h2>
            <div className="cards-container">
                <div className="card">
                   <h4>Education Advisor</h4>
                   <p>Description</p>
                </div>
                <div className="card">
                   <h4>Job Advisor</h4>
                   <p>Description</p>
                </div>
                <div className="card">
                   <h4>Health Advisor</h4>
                   <p>Description</p>
                </div>
            </div>
        </div>
        );
}







.cards-container{
    display: flex;
    justify-content: center;
    align-items: center;
    margin:180px auto;
    margin-bottom: 0;
    
}

.landing h2{
    text-align:center;
    cursor: pointer;
}

.cards-container .card{
    border-radius: 6px;
    width: 300px;
    height: 220px;
    background:rgba(0, 0, 0, 0.5);
      box-shadow: 0 10px 8px rgba(0, 0, 0, 0.2);

    color: #fff;
    justify-content: center;
    margin:20px;
}

.card h4{
    text-align:center;
}
.card p{
    text-align: center;
}
