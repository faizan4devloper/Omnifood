import React, { useState } from "react";
import "./App.css"
import { BrowserRouter, Routes, Route } from "react-router-dom";

import { Header } from "./components/Landing/Header";
import { Hero } from "./components/Landing/Hero"; 
import { NewClaimPage } from "./NewClaimPage";
import { SummaryView } from "./SummaryView";
import { Footer } from "./components/Landing/Footer";


function App() {
  const [selectedDocument, setSelectedDocument] = useState(null);

  const handleDocumentSelect = (document) => {
    setSelectedDocument(document);
  };

  return (
    <BrowserRouter>
      <Header />
      
      <Routes>
        <Route path="/" element={
          <Hero onDocumentSelect={handleDocumentSelect} />
        } />
        
        <Route path="/NewClaimPage" element={
          <NewClaimPage />  
        } />
        <Route path="/summary" element={<SummaryView />} />

      </Routes>
      
      <Footer />
    </BrowserRouter>
  );
}

export default App;
