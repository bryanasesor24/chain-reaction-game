import React, { useState, useEffect, useRef } from 'react';

// Default export: ChainReactionApp
// This is a single-file React component designed to be used in a Vite + React project.
// Styling uses Tailwind classes (assumes Tailwind is installed in the project). If you don't
// want Tailwind, you can replace classes with your own CSS.

export default function ChainReactionApp() {
  // Room & host
  const [roomCode, setRoomCode] = useState('');
  const [isHost, setIsHost] = useState(false);

  // Teams structure: { id, name, players: [{id,name}], score, chain: [word], revealed: [[bools per letter]], solved }
  const [teams, setTeams] = useState(() => [
    { id: 'teamA', name: 'Team A', players: [], score: 0, chain: [], revealed: [], solved: false, contributions: {} },
    { id: 'teamB', name: 'Team B', players: [], score: 0, chain: [], revealed: [], solved: false, contributions: {} }
  ]);

  const [activeTeamIdx, setActiveTeamIdx] = useState(0);
  const [currentInput, setCurrentInput] = useState('');
  const [message, setMessage] = useState('');
  const inputRef = useRef(null);

  // MVP tracking
  const [mvp, setMvp] = useState(null);

  useEffect(() => {
    // focus input when it's visible
    if (inputRef.current) inputRef.current.focus();
  }, [activeTeamIdx]);

  // Utilities
  function generateRoomCode() {
    const code = Math.random().toString(36).slice(2, 8).toUpperCase();
    setRoomCode(code);
    setIsHost(true);
    setMessage(`Room created: ${code} — share code with players`);
  }

  function addPlayerToTeam(teamIdx, playerName) {
    if (!playerName) return;
    setTeams(prev => {
      const copy = JSON.parse(JSON.stringify(prev));
      const id = 'p' + Date.now();
      copy[teamIdx].players.push({ id, name: playerName });
      return copy;
    });
  }

  function setTeamChain(teamIdx, chainString) {
    // chainString: newline-separated words OR comma-separated
    const words = chainString
      .split(/[,\n]+/)
      .map(w => w.trim())
      .filter(Boolean);
    setTeams(prev => {
      const copy = JSON.parse(JSON.stringify(prev));
      copy[teamIdx].chain = words;
      copy[teamIdx].revealed = words.map(w => {
        // reveal first letter and full first and last words (per requirement)
        return Array.from(w).map((ch, i) => i === 0 || i === (w.length - 1) ? true : false);
      });
      copy[teamIdx].solved = false;
      copy[teamIdx].contributions = {};
      return copy;
    });
  }

  function revealOneLetter(teamIdx, wordIdx) {
    setTeams(prev => {
      const copy = JSON.parse(JSON.stringify(prev));
      const revealed = copy[teamIdx].revealed[wordIdx];
      for (let i = 0; i < revealed.length; i++) {
        if (!revealed[i]) {
          revealed[i] = true;
          break;
        }
      }
      return copy;
    });
  }

  function handleSubmitAnswer(teamIdx, playerId) {
    const input = currentInput.trim();
    if (!input) return setMessage('Please type an answer.');
    const team = teams[teamIdx];
    // Check against any unrevealed words (except ones already fully revealed)
    const matchIndex = team.chain.findIndex((w, idx) => {
      const normalized = w.toLowerCase();
      return normalized === input.toLowerCase() && !team.revealed[idx].every(Boolean);
    });

    if (matchIndex !== -1) {
      // correct
      setTeams(prev => {
        const copy = JSON.parse(JSON.stringify(prev));
        const w = copy[teamIdx].chain[matchIndex];
        // reveal all letters for that word
        copy[teamIdx].revealed[matchIndex] = Array.from(w).map(() => true);
        copy[teamIdx].score += 100; // arbitrary points per correct word
        // contribution tracking
        if (!copy[teamIdx].contributions[playerId]) copy[teamIdx].contributions[playerId] = 0;
        copy[teamIdx].contributions[playerId] += 1;
        return copy;
      });

      setMessage('Correct!');
      setCurrentInput('');
      // check if team solved all words
      setTimeout(() => {
        const t = teams[teamIdx];
        const allSolved = t.chain.length > 0 && t.chain.every((w, idx) => teams[teamIdx].revealed[idx] && teams[teamIdx].revealed[idx].every(Boolean));
        // note: because teams state hasn't updated yet in this closure, recalc after small delay
        setTimeout(() => {
          setTeams(prev => {
            const copy = JSON.parse(JSON.stringify(prev));
            const all = copy[teamIdx].chain.length > 0 && copy[teamIdx].chain.every((w, idx) => copy[teamIdx].revealed[idx].every(Boolean));
            if (all) copy[teamIdx].solved = true;
            return copy;
          });
        }, 60);

      }, 50);
    } else {
      // wrong — reveal one letter in the first unrevealed word
      const unrevealedIdx = team.chain.findIndex((w, idx) => !team.revealed[idx].every(Boolean));
      if (unrevealedIdx === -1) {
        setMessage('No more words to guess for this team.');
        return;
      }
      revealOneLetter(teamIdx, unrevealedIdx);
      setMessage('Wrong — a letter was revealed.');
      setCurrentInput('');
    }
  }

  function nextTurn() {
    setActiveTeamIdx((activeTeamIdx + 1) % teams.length);
    setMessage('Next team is up.');
  }

  function computeMVPForTeam(teamIdx) {
    const t = teams[teamIdx];
    let best = null;
    Object.entries(t.contributions || {}).forEach(([pid, count]) => {
      if (!best || count > best.count) best = { id: pid, count };
    });
    return best;
  }

  function endRound() {
    // determine MVP among all teams
    let overall = null;
    teams.forEach((t, idx) => {
      const m = computeMVPForTeam(idx);
      if (m && (!overall || m.count > overall.count)) overall = { teamIdx: idx, ...m };
    });
    if (overall) {
      const player = teams[overall.teamIdx].players.find(p => p.id === overall.id);
      setMvp({ teamName: teams[overall.teamIdx].name, playerName: player ? player.name : 'Unknown', count: overall.count });
    } else {
      setMvp(null);
    }
    // reset solved flags for next round (host-controlled in real flow)
    setTeams(prev => prev.map(t => ({ ...t, solved: false, contributions: {} })));
    setMessage('Round ended. MVP shown.');
  }

  // Host UI controls state
  const [team0Input, setTeam0Input] = useState('Tooth,Brush,Hair,Cut,Line,Up');
  const [team1Input, setTeam1Input] = useState('Apple,Fruit,Leaf,Boot');
  const [newPlayerName, setNewPlayerName] = useState('');

  // join as player locally (no networking) — convenience to test
  function joinAsPlayer(teamIdx) {
    if (!newPlayerName.trim()) return setMessage('Type a name and press Join');
    addPlayerToTeam(teamIdx, newPlayerName.trim());
    setNewPlayerName('');
    setMessage('Player added locally for testing');
  }

  return (
    <div className="min-h-screen bg-gradient-to-b from-slate-900 to-slate-800 text-white p-6">
      <div className="max-w-6xl mx-auto">
        <header className="flex items-center justify-between mb-6">
          <h1 className="text-4xl font-extrabold tracking-tight">Chain Reaction — Halloween Mockup</h1>
          <div className="text-right">
            <div className="mb-1">Room: <strong className="ml-2">{roomCode || '---'}</strong></div>
            <div className="space-x-2">
              <button className="px-3 py-1 rounded bg-orange-500 text-black" onClick={generateRoomCode}>Create Room</button>
              <button className="px-3 py-1 rounded bg-slate-700" onClick={() => { setRoomCode(''); setIsHost(false); setMessage('Left room'); }}>Leave</button>
            </div>
          </div>
        </header>

        <main className="grid grid-cols-1 md:grid-cols-3 gap-6">
          <section className="md:col-span-2">
            <div className="grid grid-cols-2 gap-4">
              {teams.map((team, idx) => (
                <div key={team.id} className={`p-4 rounded-lg border ${activeTeamIdx === idx ? 'border-orange-400 shadow-lg' : 'border-slate-700'}`}>
                  <div className="flex justify-between items-center mb-3">
                    <h2 className="text-xl font-semibold">{team.name}</h2>
                    <div className="text-2xl font-bold">{team.score}</div>
                  </div>

                  <div className="space-y-2">
                    <div className="text-sm">Players:</div>
                    <ul className="mb-2">
                      {team.players.length === 0 ? <li className="text-slate-400">(no players)</li> : team.players.map(p => <li key={p.id}>{p.name}</li>)}
                    </ul>

                    <div className="bg-slate-900 p-2 rounded">
                      {/* Puzzle grid: show each chain word as boxes */}
                      {team.chain.length === 0 ? (
                        <div className="text-slate-400">No chain set</div>
                      ) : (
                        <div className="space-y-2">
                          {team.chain.map((word, widx) => (
                            <div key={widx} className="flex items-center">
                              <div className="w-20 text-sm">{widx === 0 || widx === team.chain.length - 1 ? <em>given</em> : `#${widx}`}</div>
                              <div className="flex gap-1">
                                {Array.from(word).map((ch, i) => {
                                  const revealed = team.revealed[widx] && team.revealed[widx][i];
                                  return (
                                    <div key={i} className={`w-8 h-8 flex items-center justify-center border rounded ${revealed ? 'bg-green-600' : 'bg-slate-700'}`}>
                                      {revealed ? ch.toUpperCase() : '_'}
                                    </div>
                                  );
                                })}
                              </div>
                            </div>
                          ))}
                        </div>
                      )}
                    </div>

                  </div>
                </div>
              ))}
            </div>

            <div className="mt-4 p-4 rounded bg-slate-900">
              <div className="flex items-center gap-3">
                <div className="flex-1">
                  <input ref={inputRef} value={currentInput} onChange={e => setCurrentInput(e.target.value)} placeholder={teams[activeTeamIdx].chain.length ? 'Type your guess here' : 'No puzzle set'} className="w-full p-2 rounded bg-slate-800" />
                </div>
                <div>
                  <button className="px-4 py-2 rounded bg-indigo-600" onClick={() => handleSubmitAnswer(activeTeamIdx, teams[activeTeamIdx].players[0]?.id || 'local')}>Submit</button>
                </div>
                <div>
                  <button className="px-4 py-2 rounded bg-orange-500" onClick={nextTurn}>End Turn</button>
                </div>
              </div>
              <div className="mt-2 text-slate-300">{message}</div>
            </div>

          </section>

          <aside className="p-4 rounded-lg bg-slate-900">
            <h3 className="text-lg font-semibold mb-2">Host Controls (local demo)</h3>
            <div className="mb-2">
              <label className="block text-xs">Team A chain (comma or newline separated)</label>
              <textarea className="w-full p-2 bg-slate-800 rounded" value={team0Input} onChange={e => setTeam0Input(e.target.value)} rows={3}></textarea>
              <div className="flex gap-2 mt-2">
                <button className="px-3 py-1 rounded bg-green-600" onClick={() => setTeamChain(0, team0Input)}>Set Team A Chain</button>
                <button className="px-3 py-1 rounded bg-red-600" onClick={() => setTeams(prev => { const c = JSON.parse(JSON.stringify(prev)); c[0].chain = []; c[0].revealed = []; return c; })}>Clear</button>
              </div>
            </div>

            <div className="mb-2">
              <label className="block text-xs">Team B chain (comma or newline separated)</label>
              <textarea className="w-full p-2 bg-slate-800 rounded" value={team1Input} onChange={e => setTeam1Input(e.target.value)} rows={3}></textarea>
              <div className="flex gap-2 mt-2">
                <button className="px-3 py-1 rounded bg-green-600" onClick={() => setTeamChain(1, team1Input)}>Set Team B Chain</button>
                <button className="px-3 py-1 rounded bg-red-600" onClick={() => setTeams(prev => { const c = JSON.parse(JSON.stringify(prev)); c[1].chain = []; c[1].revealed = []; return c; })}>Clear</button>
              </div>
            </div>

            <div className="mb-2">
              <label className="block text-xs">Add test player</label>
              <div className="flex gap-2">
                <input className="flex-1 p-2 rounded bg-slate-800" placeholder="Player name" value={newPlayerName} onChange={e => setNewPlayerName(e.target.value)} />
                <button className="px-3 py-1 rounded bg-indigo-600" onClick={() => joinAsPlayer(0)}>Join Team A</button>
                <button className="px-3 py-1 rounded bg-indigo-600" onClick={() => joinAsPlayer(1)}>Join Team B</button>
              </div>
            </div>

            <div className="flex gap-2 mt-4">
              <button className="px-3 py-1 rounded bg-yellow-500" onClick={endRound}>End Round (Show MVP)</button>
              <button className="px-3 py-1 rounded bg-slate-700" onClick={() => { setMvp(null); setMessage('MVP cleared'); }}>Clear MVP</button>
            </div>

            <div className="mt-4">
              <h4 className="text-sm">MVP</h4>
              {mvp ? (
                <div className="mt-2 p-2 bg-slate-800 rounded">
                  <div className="font-semibold">{mvp.playerName}</div>
                  <div className="text-sm">Team: {mvp.teamName}</div>
                  <div className="text-sm">Correct answers: {mvp.count}</div>
                </div>
              ) : (
                <div className="text-slate-400">No MVP yet</div>
              )}
            </div>

          </aside>
        </main>

        <footer className="mt-8 text-sm text-slate-400">
          Local demo: this app runs entirely in the browser (no server). For remote players connect the hosted app URL and use the Room code flow (requires backend/session service or a hosted public site).
        </footer>
      </div>
    </div>
  );
}

/*
README (setup & deployment)

1) Create a new Vite React project (recommended):

   npm create vite@latest chain-reaction -- --template react
   cd chain-reaction
   npm install

2) Install Tailwind (optional but recommended for styling):

   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init -p

   // tailwind.config.cjs -> configure content paths
   // Add Tailwind directives to src/index.css:
   // @tailwind base; @tailwind components; @tailwind utilities;

3) Replace src/App.jsx with the contents of this file (or import this component)
   If using a single-file approach place this as src/App.jsx and ensure imports/exports match.

4) Run locally:

   npm run dev

5) To allow remote players to join from different locations you must deploy the site to a public host
   (Vercel, Netlify, or Firebase Hosting). Deployments are straightforward with Vercel (connect the GitHub repo and push).

6) For a production multi-player experience with real-time shared state use a backend or realtime DB:
   - Option A (easier): Firebase Realtime Database or Firestore + simple security rules
   - Option B: Supabase Realtime
   - Option C: WebSocket server (Node + Socket.io)

   You would store the room object (room code, teams, players, chain state) in the realtime store and sync updates between clients.

Notes & next steps:
- This demo operates locally (no networking). The Host Controls are intentionally in-page for quick testing.
- If you'd like I can produce a Socket.io backend (Node/Express) and wire up the client to run a real multiplayer session. That will include room creation, join-by-code, and proper host privileges.
*/
