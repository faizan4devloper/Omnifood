.selected-question.expanded p{
    
}
const toggleExpandDescription = (question, index) => {
  const newExpandedDescriptions = {};
  newExpandedDescriptions[`${question}-${index}`] = !expandedDescriptions[`${question}-${index}`];

  // Collapse all other descriptions under the same question
  questionDescriptions[question].forEach((_, idx) => {
    if (idx !== index) {
      newExpandedDescriptions[`${question}-${idx}`] = false;
    }
  });

  setExpandedDescriptions(newExpandedDescriptions);
};
