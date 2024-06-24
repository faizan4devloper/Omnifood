import React, { useState } from "react";
import "./Insights.css";

export function Insights() {
    const [localities] = useState(["New York", "Los Angeles", "Chicago", "Houston", "Phoenix"]);
    const [selectedLocality, setSelectedLocality] = useState("");

    const handleLocalityChange = (event) => {
        setSelectedLocality(event.target.value);
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            <div className="locality-section">
                <h4>Choose Your Locality</h4>
                <select 
                    className="locality-dropdown" 
                    value={selectedLocality} 
                    onChange={handleLocalityChange}
                >
                    <option value="" disabled>Select a locality</option>
                    {localities.map((locality, index) => (
                        <option key={index} value={locality}>
                            {locality}
                        </option>
                    ))}
                </select>
                {selectedLocality && <div className="selected-message">You selected: {selectedLocality}</div>}
            </div>
        </div>
    );
}








.insights-container {
    background-color: rgba(0, 0, 0, 0.5);
    margin: 80px 0 0 10px;
    border-radius: 10px;
    width: 400px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease-in-out;
}

.insights-container:hover {
    transform: scale(1.02);
}

.insights-container h3 {
    text-align: center;
    color: #fff;
}

.locality-section {
    margin-top: 20px;
    text-align: center;
}

.locality-section h4 {
    color: #fff;
    margin-bottom: 10px;
}

.locality-dropdown {
    width: 80%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 1em;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.locality-dropdown:hover {
    background-color: #f1f1f1;
}

.selected-message {
    margin-top: 15px;
    color: #fff;
    font-size: 1.2em;
    animation: fadeIn 0.5s ease-in-out;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
