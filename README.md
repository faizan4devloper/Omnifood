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
    background: rgba(245, 245, 245);
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
    margin-top: 20px;
    
}

.card p {
    position: relative;
    z-index: 1;
    text-align: center;
    color: #ddd; /* Color for the description */
    margin: 10px 20px;
}
