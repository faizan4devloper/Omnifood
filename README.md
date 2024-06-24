import React, { useState } from "react";
import Select from "react-select";
import "./Insights.css";

export function Insights() {
    const [localities] = useState([
        { value: "New York", label: "New York" },
        { value: "Los Angeles", label: "Los Angeles" },
        { value: "Chicago", label: "Chicago" },
        { value: "Houston", label: "Houston" },
        { value: "Phoenix", label: "Phoenix" }
    ]);
    const [selectedLocality, setSelectedLocality] = useState(null);

    const handleLocalityChange = (selectedOption) => {
        setSelectedLocality(selectedOption);
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            <div className="locality-section">
                <h4>Choose Your Locality</h4>
                <Select
                    className="dropdown"
                    value={selectedLocality}
                    onChange={handleLocalityChange}
                    options={localities}
                    placeholder="Select a locality"
                    isClearable
                />
                {selectedLocality && <div className="selected-message">You selected: {selectedLocality.label}</div>}
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

.dropdown {
    width: 100%;
    margin-bottom: 20px;
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

/* Custom styles for react-select */
.react-select__control {
    background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    color: white;
    border: none;
    border-radius: 5px;
    box-shadow: none;
}

.react-select__menu {
    background-color: white;
    border-radius: 5px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.react-select__option--is-focused {
    background-color: #f1f1f1;
}

.react-select__option--is-selected {
    background-color: #1f77f6;
    color: white;
}
