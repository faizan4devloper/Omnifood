import React, { useState } from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import "./App.css";

import { Header } from "./components/Landing/Header";
import { Hero } from "./components/Landing/Hero"; 
import { NewClaimPage } from "./components/NewClaimPage";
import { SummaryView } from "./components/SummaryView";
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
        <Route path="/" element={<Hero onDocumentSelect={handleDocumentSelect} />} />
        <Route path="/NewClaimPage" element={<NewClaimPage />} />
        <Route path="/summary" element={<SummaryView />} />
      </Routes>
      <Footer />
    </BrowserRouter>
  );
}

export default App;
