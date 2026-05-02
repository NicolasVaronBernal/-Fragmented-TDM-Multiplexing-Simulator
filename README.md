# 🛰️ BIT-FRAGMENTATION TDM SIMULATOR

# 📖 Overview
This repository hosts an interactive Time Division Multiplexing (TDM) 
simulator designed to visualize synchronous data communication through 
granular bit-level fragmentation. It provides a low-level demonstration 
of how multiple data streams are interleaved into a single serial flow.

# 🌟 Key Features
- Variable Fragmentation: Divide 8-bit bytes into 1, 2, 4, or 8 parts.
- Automatic Bit-Padding: Synchronizes channels by prepending null bits.
- Real-Time Processing: Reactive UI updates binary conversion as you type.
- Visual Pipeline: Input -> Binary -> TDM Frames -> Serial Stream.

# 🛠️ Technical Implementation: Core TDM Algorithm
/* 
   Interleaves bit fragments from multiple sources into a single stream.
*/
function processTDM(channels, fragments) {
    const maxChars = Math.max(...channels.map(c => c.length));
    const bitsPerFragment = 8 / fragments;
    let finalSerialStream = "";

    for (let t = 0; t < maxChars; t++) {
        for (let f = 0; f < fragments; f++) {
            channels.forEach((content, chIdx) => {
                const paddingNeeded = maxChars - content.length;
                let charBits = (t >= paddingNeeded) 
                    ? getBits(content[t - paddingNeeded]) 
                    : "00000000";

                const start = f * bitsPerFragment;
                const chunk = charBits.substring(start, start + bitsPerFragment);
                finalSerialStream += chunk;
            });
        }
    }
    return finalSerialStream;
}

# 🚀 Getting Started
# 1. Clone the repository: git clone https://github.com/your-user/bit-tdm-simulator.git
# 2. Navigate to the directory: cd bit-tdm-simulator
# 3. Launch the application: open index.html (in any modern browser)

# 🎮 How to Use
1. Enter Data: Type into any of the available input channels (A, B, or C).
2. Select Granularity: Use the top-bar buttons (1, 2, 4, or 8) to choose 
   how many fragments each byte should be split into.
3. Inspect Frames: Scroll through the "Structure of Frames" section to 
   see exactly how bits from different channels are grouped.
4. Analyze Output: View the final binary stream in the terminal-style 
   output at the bottom.

# 🏗️ Built With
{
  "Frontend": "HTML5, JavaScript (ES6+)",
  "Styling": "Tailwind CSS (via CDN)",
  "Typography": ["Inter", "Fira Code"],
  "Architecture": "Single-file Component (SFC) design"
}

# 🎓 Academic Context
This project was developed as a pedagogical resource for University students 
majoring in Computer Systems Engineering. It aims to facilitate the 
understanding of:
- Data Communication Foundations
- Hierarchical Multiplexing Logic
- Bit-level Data Fragmentation
- Synchronous System-Level Automation
