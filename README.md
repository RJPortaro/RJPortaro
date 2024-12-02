- 👋 Hi, I’m @RJPortaro
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
RJPortaro/RJPortaro is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->import React, { useState, useRef } from 'react';

const DeclinedLoanResponseWheel = () => {
  const declineResponses = [
    "I think it's a Pass",
    "Lets see how your FYE statements look",
    "How would you like to collateralize your request?",
    "We don't have a product fit for this type of business",
    "Unfortunately, we don't lend outside of our footprint",
    "Have you considered an SBA loan",
    "Are you familiar with Factoring",
    "We are not super comfortable with the request",
    "Would you be open to me referring you to another lender",
    "4.0x leverage is a bit rich for our comfort level",
    "Have you heard of BallparkMarkets?"
  ];

  const colors = [
    'bg-red-500', 'bg-orange-500', 'bg-yellow-500', 
    'bg-green-500', 'bg-blue-500', 'bg-purple-500', 
    'bg-pink-500', 'bg-teal-500', 'bg-indigo-500', 
    'bg-emerald-500', 'bg-cyan-500'
  ];

  const [spinning, setSpinning] = useState(false);
  const [selectedResponse, setSelectedResponse] = useState(null);
  const wheelRef = useRef(null);

  const spinWheel = () => {
    if (!spinning) {
      setSpinning(true);
      setSelectedResponse(null);

      const spinDuration = Math.floor(Math.random() * 2000) + 3000;
      
      if (wheelRef.current) {
        wheelRef.current.style.transition = `transform ${spinDuration}ms cubic-bezier(0.25, 0.1, 0.25, 1)`;
        wheelRef.current.style.transform = `rotate(${Math.floor(Math.random() * 720) + 1080}deg)`;
      }

      setTimeout(() => {
        const randomIndex = Math.floor(Math.random() * declineResponses.length);
        setSelectedResponse(declineResponses[randomIndex]);
        setSpinning(false);
        
        if (wheelRef.current) {
          wheelRef.current.style.transition = 'none';
          wheelRef.current.style.transform = 'rotate(0deg)';
        }
      }, spinDuration);
    }
  };

  return (
    <div className="flex flex-col items-center p-6 bg-gray-50 rounded-lg shadow-lg">
      <h2 className="text-3xl font-bold mb-6 text-gray-800">Banker Response Wheel</h2>
      
      <div 
        ref={wheelRef}
        className="relative w-96 h-96 rounded-full border-8 border-gray-300 shadow-2xl overflow-hidden"
      >
        <div className="absolute inset-0 flex flex-wrap">
          {declineResponses.map((response, index) => (
            <div 
              key={response}
              className={`w-1/2 h-1/6 flex items-center justify-center 
                text-xs font-semibold text-white p-2 ${colors[index % colors.length]}`}
              style={{
                transform: `rotate(${index * (360 / declineResponses.length)}deg)`,
                transformOrigin: 'bottom center'
              }}
            >
              {response}
            </div>
          ))}
        </div>
        
        <div className="absolute inset-0 flex items-center justify-center">
          {!spinning && (
            <button 
              onClick={spinWheel} 
              className="z-10 bg-white text-red-600 px-6 py-3 rounded-full 
                shadow-lg hover:bg-red-50 transition duration-300 
                font-bold uppercase tracking-wider"
            >
              Spin Wheel
            </button>
          )}
        </div>
      </div>

      {selectedResponse && (
        <div className="mt-6 text-xl font-bold text-red-700 
          bg-red-100 px-4 py-2 rounded-lg shadow-md text-center">
          {selectedResponse}
        </div>
      )}
    </div>
  );
};

export default DeclinedLoanResponseWheel;
