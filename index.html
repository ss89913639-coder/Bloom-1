import { useState, useEffect, useRef, useCallback } from "react";

// ────────────────────────────────────────────────────────────────
// FIREBASE-LIKE IN-MEMORY STORE (persistent via localStorage)
// ────────────────────────────────────────────────────────────────
const STORAGE_KEY = "jaeneung_db";

function loadDB() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) return JSON.parse(raw);
  } catch {}
  return {
    users: {},        // uid -> { uid, id, pw, nickname, talents: [], completedLectures: [] }
    lectures: [],     // { id, title, category, desc, slots: 3, enrolled: [], date, mode: 'talent'|'hint', hint: '' }
    reviews: {},      // lectureId -> [{ uid, nickname, star, text, ts }]
    mode: "talent",   // global default mode
    session: null,    // { uid }
  };
}

function saveDB(db) {
  try { localStorage.setItem(STORAGE_KEY, JSON.stringify(db)); } catch {}
}

// ────────────────────────────────────────────────────────────────
// TALENT DATA
// ────────────────────────────────────────────────────────────────
const TALENT_STAGES = ["씨앗", "새싹", "개화"];
const TALENT_ICONS = { "씨앗": "🌱", "새싹": "🌿", "개화": "🌸" };
const CATEGORY_META = {
  "연기": { icon: "🎭", color: "#c084fc" },
  "음악": { icon: "🎵", color: "#f472b6" },
  "미술": { icon: "🎨", color: "#fb923c" },
  "스포츠": { icon: "⚡", color: "#4ade80" },
  "요리": { icon: "🔥", color: "#fbbf24" },
  "경영": { icon: "📊", color: "#60a5fa" },
  "외국어": { icon: "🌐", color: "#34d399" },
  "기술": { icon: "⚙️", color: "#94a3b8" },
};

// ────────────────────────────────────────────────────────────────
// MINI-GAMES
// ────────────────────────────────────────────────────────────────
function TimingGame({ onComplete }) {
  const [pos, setPos] = useState(0);
  const [dir, setDir] = useState(1);
  const [result, setResult] = useState(null);
  const rafRef = useRef();
  const lastRef = useRef(0);

  useEffect(() => {
    let p = 0, d = 1;
    const tick = (ts) => {
      if (ts - lastRef.current > 16) {
        p += d * 2;
        if (p >= 100 || p <= 0) d *= -1;
        setPos(p); setDir(d);
        lastRef.current = ts;
      }
      rafRef.current = requestAnimationFrame(tick);
    };
    rafRef.current = requestAnimationFrame(tick);
    return () => cancelAnimationFrame(rafRef.current);
  }, []);

  const click = () => {
    cancelAnimationFrame(rafRef.current);
    const success = pos >= 35 && pos <= 65;
    setResult(success);
    setTimeout(() => onComplete(success), 1000);
  };

  return (
    <div style={{ textAlign: "center" }}>
      <p style={{ color: "#a0a0b0", marginBottom: 16, fontSize: 13 }}>게이지가 <span style={{ color: "#c084fc" }}>청색 구간</span> 안에 있을 때 클릭하세요</p>
      <div style={{ position: "relative", height: 24, background: "#1a1a2e", borderRadius: 12, margin: "0 auto 20px", width: "100%", overflow: "hidden" }}>
        <div style={{ position: "absolute", left: "35%", width: "30%", height: "100%", background: "rgba(96,165,250,0.3)", borderRadius: 12 }} />
        <div style={{ position: "absolute", top: 4, left: `${pos}%`, width: 16, height: 16, background: result === null ? "#fff" : result ? "#4ade80" : "#f87171", borderRadius: "50%", transform: "translateX(-50%)", transition: "background 0.2s" }} />
      </div>
      {result === null
        ? <button onClick={click} style={btnStyle("#c084fc")}>클릭!</button>
        : <p style={{ color: result ? "#4ade80" : "#f87171", fontWeight: 700, fontSize: 18 }}>{result ? "성공!" : "실패..."}</p>}
    </div>
  );
}

function TypingGame({ onComplete }) {
  const CODES = ["BLOOM", "TALENT", "GAEHWA", "FLOWER", "AWAKEN"];
  const [code] = useState(() => CODES[Math.floor(Math.random() * CODES.length)]);
  const [input, setInput] = useState("");
  const [timeLeft, setTimeLeft] = useState(10);
  const [done, setDone] = useState(false);

  useEffect(() => {
    if (done) return;
    const t = setInterval(() => {
      setTimeLeft(p => {
        if (p <= 1) { clearInterval(t); setDone(true); setTimeout(() => onComplete(false), 800); return 0; }
        return p - 1;
      });
    }, 1000);
    return () => clearInterval(t);
  }, [done]);

  const handleChange = (e) => {
    const v = e.target.value.toUpperCase();
    setInput(v);
    if (v === code) { setDone(true); setTimeout(() => onComplete(true), 600); }
  };

  return (
    <div style={{ textAlign: "center" }}>
      <p style={{ color: "#a0a0b0", fontSize: 13, marginBottom: 12 }}>제한 시간 내에 정확히 입력하세요</p>
      <div style={{ fontSize: 32, letterSpacing: 8, color: "#c084fc", fontFamily: "monospace", marginBottom: 16, fontWeight: 700 }}>{code}</div>
      <div style={{ marginBottom: 12, color: timeLeft <= 3 ? "#f87171" : "#a0a0b0", fontSize: 13 }}>⏱ {timeLeft}초</div>
      <input
        disabled={done}
        value={input}
        onChange={handleChange}
        style={{ background: "#1a1a2e", border: "1px solid #333", color: "#fff", padding: "8px 16px", borderRadius: 8, fontSize: 18, textAlign: "center", letterSpacing: 4, width: "100%", fontFamily: "monospace" }}
        autoFocus
      />
    </div>
  );
}

function ReactionGame({ onComplete }) {
  const [state, setState] = useState("wait"); // wait | ready | click | done
  const [result, setResult] = useState(null);
  const timerRef = useRef();

  useEffect(() => {
    const delay = 1500 + Math.random() * 2000;
    timerRef.current = setTimeout(() => setState("ready"), delay);
    return () => clearTimeout(timerRef.current);
  }, []);

  const handleClick = () => {
    if (state === "wait") { setResult(false); setState("done"); setTimeout(() => onComplete(false), 800); }
    else if (state === "ready") { setResult(true); setState("done"); setTimeout(() => onComplete(true), 800); }
  };

  return (
    <div style={{ textAlign: "center" }}>
      <p style={{ color: "#a0a0b0", fontSize: 13, marginBottom: 20 }}>신호가 켜지면 즉시 클릭하세요!</p>
      <div
        onClick={handleClick}
        style={{
          width: 120, height: 120, borderRadius: "50%", margin: "0 auto 20px",
          background: state === "ready" ? "#4ade80" : state === "done" ? (result ? "#4ade80" : "#f87171") : "#333",
          cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center",
          fontSize: 13, color: "#fff", transition: "background 0.15s",
          boxShadow: state === "ready" ? "0 0 40px #4ade8088" : "none"
        }}
      >
        {state === "wait" ? "대기 중..." : state === "ready" ? "지금!" : result ? "성공!" : "실패!"}
      </div>
    </div>
  );
}

const GAMES = [TimingGame, TypingGame, ReactionGame];

function MiniGame({ onComplete }) {
  const [Game] = useState(() => GAMES[Math.floor(Math.random() * GAMES.length)]);
  return (
    <div style={{ background: "#0d0d1a", border: "1px solid #2a2a3e", borderRadius: 16, padding: 24 }}>
      <h3 style={{ color: "#c084fc", marginBottom: 20, textAlign: "center", fontFamily: "'Noto Serif KR', serif" }}>재능 수련</h3>
      <Game onComplete={onComplete} />
    </div>
  );
}

// ────────────────────────────────────────────────────────────────
// HELPERS
// ────────────────────────────────────────────────────────────────
function btnStyle(color = "#c084fc", small = false) {
  return {
    background: color, color: "#fff", border: "none", borderRadius: small ? 6 : 10,
    padding: small ? "6px 14px" : "10px 24px", cursor: "pointer", fontWeight: 700,
    fontSize: small ? 12 : 14, fontFamily: "inherit",
  };
}

function StarRating({ value, onChange }) {
  return (
    <div style={{ display: "flex", gap: 4 }}>
      {[1, 2, 3, 4, 5].map(s => (
        <span
          key={s}
          onClick={() => onChange && onChange(s)}
          style={{ fontSize: 22, cursor: onChange ? "pointer" : "default", color: s <= value ? "#fbbf24" : "#333" }}
        >★</span>
      ))}
    </div>
  );
}

function Modal({ children, onClose }) {
  return (
    <div style={{
      position: "fixed", inset: 0, background: "rgba(0,0,0,0.7)", zIndex: 999,
      display: "flex", alignItems: "center", justifyContent: "center", padding: 20,
    }} onClick={e => e.target === e.currentTarget && onClose()}>
      <div style={{ background: "#0f0f1e", border: "1px solid #2a2a3e", borderRadius: 20, padding: 28, maxWidth: 480, width: "100%", maxHeight: "90vh", overflowY: "auto" }}>
        {children}
      </div>
    </div>
  );
}

// ────────────────────────────────────────────────────────────────
// MAIN APP
// ────────────────────────────────────────────────────────────────
export default function App() {
  const [db, setDB] = useState(loadDB);
  const [page, setPage] = useState("home"); // home | lobby | mypage | admin
  const [authMode, setAuthMode] = useState("login");
  const [form, setForm] = useState({ id: "", pw: "", nickname: "" });
  const [error, setError] = useState("");
  const [selectedLecture, setSelectedLecture] = useState(null);
  const [gamePhase, setGamePhase] = useState(null); // null | 'playing' | 'review'
  const [reviewForm, setReviewForm] = useState({ star: 5, text: "" });
  const [toast, setToast] = useState(null);
  const [adminTab, setAdminTab] = useState("lectures");
  const [newLecture, setNewLecture] = useState({ title: "", category: "연기", desc: "", mode: "talent", hint: "" });
  const [globalMode, setGlobalMode] = useState(db.mode || "talent");

  const persist = useCallback((updater) => {
    setDB(prev => {
      const next = typeof updater === "function" ? updater(prev) : { ...prev, ...updater };
      saveDB(next);
      return next;
    });
  }, []);

  const showToast = (msg, ok = true) => {
    setToast({ msg, ok });
    setTimeout(() => setToast(null), 2500);
  };

  const me = db.session ? db.users[db.session.uid] : null;
  const isAdmin = me?.id === "admin";

  // ── AUTH ──
  const handleLogin = () => {
    const user = Object.values(db.users).find(u => u.id === form.id && u.pw === form.pw);
    if (!user) { setError("아이디 또는 비밀번호가 틀렸습니다."); return; }
    persist(p => ({ ...p, session: { uid: user.uid } }));
    setPage("lobby"); setError("");
  };

  const handleRegister = () => {
    if (!form.id || !form.pw || !form.nickname) { setError("모든 항목을 입력하세요."); return; }
    if (Object.values(db.users).find(u => u.id === form.id)) { setError("이미 사용 중인 아이디입니다."); return; }
    const uid = Date.now().toString();
    persist(p => ({ ...p, users: { ...p.users, [uid]: { uid, id: form.id, pw: form.pw, nickname: form.nickname, talents: [], completedLectures: [] } }, session: { uid } }));
    setPage("lobby"); setError("");
  };

  const logout = () => { persist(p => ({ ...p, session: null })); setPage("home"); };

  // ── LECTURE ENROLL & GAME ──
  const startLecture = (lecture) => {
    if (!me) return;
    if (lecture.enrolled.includes(me.uid)) { showToast("이미 수강한 강의입니다.", false); return; }
    if (me.completedLectures.includes(lecture.id)) { showToast("이미 수강 완료한 강의입니다.", false); return; }
    if (lecture.enrolled.length >= lecture.slots) { showToast("수강 인원이 마감되었습니다.", false); return; }
    setSelectedLecture(lecture);
    setGamePhase("playing");
  };

  const onGameComplete = (success) => {
    if (!success) {
      showToast("수련에 실패했습니다. 다시 도전해 보세요.", false);
      setGamePhase(null); setSelectedLecture(null); return;
    }
    // Enroll + grant talent/hint
    const lec = selectedLecture;
    const effectiveMode = lec.mode || db.mode;

    persist(prev => {
      const user = { ...prev.users[me.uid] };
      user.completedLectures = [...(user.completedLectures || []), lec.id];

      if (effectiveMode === "talent") {
        const existing = user.talents.find(t => t.category === lec.category);
        if (existing) {
          existing.stage = Math.min(existing.stage + 1, 2);
        } else if (user.talents.length < 3) {
          user.talents = [...user.talents, { category: lec.category, stage: 0 }];
        }
      }

      const lectures = prev.lectures.map(l =>
        l.id === lec.id ? { ...l, enrolled: [...l.enrolled, me.uid] } : l
      );

      return { ...prev, users: { ...prev.users, [me.uid]: user }, lectures };
    });

    setGamePhase("review");
  };

  const submitReview = () => {
    const lec = selectedLecture;
    persist(prev => {
      const existing = prev.reviews[lec.id] || [];
      return {
        ...prev,
        reviews: {
          ...prev.reviews,
          [lec.id]: [...existing, { uid: me.uid, nickname: me.nickname, star: reviewForm.star, text: reviewForm.text, ts: Date.now() }]
        }
      };
    });
    setGamePhase(null); setSelectedLecture(null); setReviewForm({ star: 5, text: "" });
    showToast("수강을 완료했습니다!");
  };

  // ── ADMIN ──
  const addLecture = () => {
    if (!newLecture.title || !newLecture.category) return;
    const lec = { ...newLecture, id: Date.now().toString(), slots: 3, enrolled: [], date: new Date().toLocaleDateString("ko-KR") };
    persist(p => ({ ...p, lectures: [lec, ...p.lectures] }));
    setNewLecture({ title: "", category: "연기", desc: "", mode: "talent", hint: "" });
    showToast("강의가 등록되었습니다!");
  };

  const deleteLecture = (id) => {
    persist(p => ({ ...p, lectures: p.lectures.filter(l => l.id !== id) }));
  };

  const changeGlobalMode = (mode) => {
    setGlobalMode(mode);
    persist(p => ({ ...p, mode }));
    showToast(`전체 모드가 '${mode === "talent" ? "재능 발급" : "힌트 발급"}'으로 변경되었습니다!`);
  };

  // ────────────────────────────────────────────────────────────────
  // RENDER
  // ────────────────────────────────────────────────────────────────
  const today = new Date().toLocaleDateString("ko-KR");
  const todayLectures = db.lectures.filter(l => l.date === today);

  return (
    <div style={{ minHeight: "100vh", background: "#050510", color: "#e0e0f0", fontFamily: "'Noto Sans KR', sans-serif", position: "relative" }}>
      {/* Google Fonts */}
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@400;600;700&family=Noto+Sans+KR:wght@300;400;500;700&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        ::-webkit-scrollbar { width: 4px; } ::-webkit-scrollbar-track { background: #0d0d1a; } ::-webkit-scrollbar-thumb { background: #2a2a3e; border-radius: 2px; }
        input, textarea { font-family: inherit; }
        .card-hover { transition: transform 0.2s, box-shadow 0.2s; }
        .card-hover:hover { transform: translateY(-2px); box-shadow: 0 8px 32px #c084fc22; }
      `}</style>

      {/* Background decoration */}
      <div style={{ position: "fixed", inset: 0, pointerEvents: "none", overflow: "hidden", zIndex: 0 }}>
        <div style={{ position: "absolute", top: "-20%", left: "-10%", width: 500, height: 500, borderRadius: "50%", background: "radial-gradient(circle, #c084fc11 0%, transparent 70%)" }} />
        <div style={{ position: "absolute", bottom: "-20%", right: "-10%", width: 600, height: 600, borderRadius: "50%", background: "radial-gradient(circle, #818cf811 0%, transparent 70%)" }} />
      </div>

      {/* Toast */}
      {toast && (
        <div style={{ position: "fixed", top: 20, left: "50%", transform: "translateX(-50%)", zIndex: 9999, background: toast.ok ? "#1a2e1a" : "#2e1a1a", border: `1px solid ${toast.ok ? "#4ade80" : "#f87171"}`, color: toast.ok ? "#4ade80" : "#f87171", borderRadius: 10, padding: "10px 24px", fontWeight: 600, fontSize: 14, whiteSpace: "nowrap" }}>
          {toast.msg}
        </div>
      )}

      <div style={{ position: "relative", zIndex: 1 }}>
        {/* ── HOME ── */}
        {page === "home" && (
          <div style={{ minHeight: "100vh", display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center", padding: 24 }}>
            <div style={{ textAlign: "center", marginBottom: 48 }}>
              <div style={{ fontSize: 11, letterSpacing: 6, color: "#6060a0", marginBottom: 12 }}>才 能 開 花 院</div>
              <h1 style={{ fontFamily: "'Noto Serif KR', serif", fontSize: 42, fontWeight: 700, color: "#fff", marginBottom: 16, lineHeight: 1.2 }}>재능개화원</h1>
              <p style={{ color: "#6060a0", fontSize: 15, lineHeight: 1.8 }}>꿈을 포기하셨나요?<br />재능이 없는 것이 아니라,<br />아직 피어나지 않았을 뿐입니다.</p>
            </div>

            <div style={{ background: "#0f0f1e", border: "1px solid #1e1e3e", borderRadius: 20, padding: 32, width: "100%", maxWidth: 380 }}>
              <div style={{ display: "flex", marginBottom: 24, background: "#0a0a18", borderRadius: 10, padding: 4 }}>
                {["login", "register"].map(m => (
                  <button key={m} onClick={() => { setAuthMode(m); setError(""); }} style={{
                    flex: 1, padding: "8px 0", border: "none", borderRadius: 8, cursor: "pointer", fontFamily: "inherit", fontWeight: 600, fontSize: 13,
                    background: authMode === m ? "#c084fc" : "transparent", color: authMode === m ? "#fff" : "#6060a0", transition: "all 0.2s"
                  }}>{m === "login" ? "입장" : "신규 등록"}</button>
                ))}
              </div>

              {authMode === "register" && (
                <div style={{ marginBottom: 12 }}>
                  <label style={{ fontSize: 11, color: "#6060a0", marginBottom: 4, display: "block" }}>닉네임</label>
                  <input value={form.nickname} onChange={e => setForm(p => ({ ...p, nickname: e.target.value }))} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }} placeholder="표시될 이름" />
                </div>
              )}
              <div style={{ marginBottom: 12 }}>
                <label style={{ fontSize: 11, color: "#6060a0", marginBottom: 4, display: "block" }}>아이디</label>
                <input value={form.id} onChange={e => setForm(p => ({ ...p, id: e.target.value }))} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }} placeholder="아이디 입력" />
              </div>
              <div style={{ marginBottom: 20 }}>
                <label style={{ fontSize: 11, color: "#6060a0", marginBottom: 4, display: "block" }}>비밀번호</label>
                <input type="password" value={form.pw} onChange={e => setForm(p => ({ ...p, pw: e.target.value }))} onKeyDown={e => e.key === "Enter" && (authMode === "login" ? handleLogin() : handleRegister())} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }} placeholder="비밀번호 입력" />
              </div>

              {error && <p style={{ color: "#f87171", fontSize: 13, marginBottom: 16 }}>{error}</p>}

              <button onClick={authMode === "login" ? handleLogin : handleRegister} style={{ ...btnStyle("#c084fc"), width: "100%", padding: "12px 0", fontSize: 15 }}>
                {authMode === "login" ? "입장하기" : "등록 완료"}
              </button>

              {authMode === "login" && (
                <p style={{ color: "#3a3a5e", fontSize: 12, marginTop: 16, textAlign: "center" }}>
                  관리자: id <code style={{ color: "#6060a0" }}>admin</code> / pw <code style={{ color: "#6060a0" }}>admin</code>로 처음 등록하세요
                </p>
              )}
            </div>
          </div>
        )}

        {/* ── NAV (lobby / mypage / admin) ── */}
        {page !== "home" && (
          <nav style={{ position: "sticky", top: 0, zIndex: 100, background: "rgba(5,5,16,0.92)", backdropFilter: "blur(12px)", borderBottom: "1px solid #1a1a2e", padding: "0 24px" }}>
            <div style={{ maxWidth: 900, margin: "0 auto", display: "flex", alignItems: "center", gap: 8, height: 56 }}>
              <button onClick={() => setPage("lobby")} style={{ fontFamily: "'Noto Serif KR', serif", fontWeight: 700, fontSize: 18, color: "#c084fc", background: "none", border: "none", cursor: "pointer", marginRight: "auto" }}>재능개화원</button>
              {["lobby", "mypage"].map(p => (
                <button key={p} onClick={() => setPage(p)} style={{ padding: "6px 16px", background: page === p ? "#1a1a2e" : "none", border: page === p ? "1px solid #2a2a3e" : "1px solid transparent", borderRadius: 8, color: page === p ? "#c084fc" : "#6060a0", cursor: "pointer", fontSize: 13, fontFamily: "inherit" }}>
                  {p === "lobby" ? "강의실" : "마이페이지"}
                </button>
              ))}
              {isAdmin && (
                <button onClick={() => setPage("admin")} style={{ padding: "6px 16px", background: page === "admin" ? "#1a1a2e" : "none", border: page === "admin" ? "1px solid #c084fc44" : "1px solid transparent", borderRadius: 8, color: page === "admin" ? "#c084fc" : "#6060a0", cursor: "pointer", fontSize: 13, fontFamily: "inherit" }}>관리자</button>
              )}
              <button onClick={logout} style={{ padding: "6px 14px", background: "none", border: "1px solid #2a1a1a", borderRadius: 8, color: "#6060a0", cursor: "pointer", fontSize: 12, fontFamily: "inherit" }}>퇴장</button>
            </div>
          </nav>
        )}

        {/* ── LOBBY ── */}
        {page === "lobby" && (
          <div style={{ maxWidth: 900, margin: "0 auto", padding: 24 }}>
            <div style={{ marginBottom: 32 }}>
              <div style={{ fontSize: 11, letterSpacing: 4, color: "#4040a0", marginBottom: 8 }}>{today} · 오늘의 강의</div>
              <h2 style={{ fontFamily: "'Noto Serif KR', serif", fontSize: 26, color: "#fff" }}>개화원 강의실</h2>
            </div>

            {todayLectures.length === 0
              ? <div style={{ textAlign: "center", padding: 80, color: "#3a3a5e" }}>
                  <div style={{ fontSize: 40, marginBottom: 16 }}>🌱</div>
                  <p>오늘은 등록된 강의가 없습니다.</p>
                </div>
              : <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(260px, 1fr))", gap: 16 }}>
                  {todayLectures.map(lec => {
                    const meta = CATEGORY_META[lec.category] || { icon: "✦", color: "#c084fc" };
                    const spotsLeft = lec.slots - lec.enrolled.length;
                    const alreadyDone = me?.completedLectures?.includes(lec.id);
                    const effectiveMode = lec.mode || db.mode;
                    const reviews = db.reviews[lec.id] || [];
                    const avgStar = reviews.length ? (reviews.reduce((a, b) => a + b.star, 0) / reviews.length).toFixed(1) : null;
                    return (
                      <div key={lec.id} className="card-hover" style={{ background: "#0d0d1e", border: `1px solid ${alreadyDone ? "#2a2a3e" : "#1e1e3e"}`, borderRadius: 16, padding: 20, cursor: alreadyDone || spotsLeft === 0 ? "default" : "pointer", opacity: alreadyDone ? 0.6 : 1 }}
                        onClick={() => !alreadyDone && spotsLeft > 0 && startLecture(lec)}>
                        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 12 }}>
                          <span style={{ fontSize: 28 }}>{meta.icon}</span>
                          <div style={{ display: "flex", flexDirection: "column", alignItems: "flex-end", gap: 4 }}>
                            <span style={{ fontSize: 11, color: meta.color, background: meta.color + "22", borderRadius: 6, padding: "2px 8px" }}>{lec.category}</span>
                            <span style={{ fontSize: 11, color: effectiveMode === "hint" ? "#fbbf24" : "#c084fc", background: effectiveMode === "hint" ? "#fbbf2422" : "#c084fc22", borderRadius: 6, padding: "2px 8px" }}>
                              {effectiveMode === "hint" ? "💡 힌트" : "🌸 재능"}
                            </span>
                          </div>
                        </div>
                        <h3 style={{ fontFamily: "'Noto Serif KR', serif", fontSize: 16, color: "#fff", marginBottom: 6 }}>{lec.title}</h3>
                        <p style={{ fontSize: 12, color: "#5a5a7a", marginBottom: 14, lineHeight: 1.6 }}>{lec.desc}</p>
                        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                          <span style={{ fontSize: 12, color: spotsLeft === 0 ? "#f87171" : "#4ade80" }}>
                            {spotsLeft === 0 ? "마감" : `잔여 ${spotsLeft}석`}
                          </span>
                          <div style={{ display: "flex", alignItems: "center", gap: 6 }}>
                            {avgStar && <span style={{ fontSize: 12, color: "#fbbf24" }}>★ {avgStar} ({reviews.length})</span>}
                            {alreadyDone && <span style={{ fontSize: 11, color: "#4040a0" }}>수강 완료</span>}
                          </div>
                        </div>
                      </div>
                    );
                  })}
                </div>
            }

            {/* Reviews section */}
            {todayLectures.length > 0 && (
              <div style={{ marginTop: 48 }}>
                <h3 style={{ fontFamily: "'Noto Serif KR', serif", fontSize: 18, color: "#fff", marginBottom: 20 }}>수강 후기</h3>
                {todayLectures.map(lec => {
                  const reviews = db.reviews[lec.id] || [];
                  if (!reviews.length) return null;
                  return (
                    <div key={lec.id} style={{ marginBottom: 24 }}>
                      <div style={{ fontSize: 13, color: "#6060a0", marginBottom: 10 }}>「{lec.title}」</div>
                      <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
                        {reviews.map((r, i) => (
                          <div key={i} style={{ background: "#0d0d1e", border: "1px solid #1a1a2e", borderRadius: 10, padding: "12px 16px", display: "flex", alignItems: "flex-start", gap: 12 }}>
                            <div>
                              <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 4 }}>
                                <span style={{ fontSize: 13, fontWeight: 600, color: "#c084fc" }}>{r.nickname}</span>
                                <StarRating value={r.star} />
                              </div>
                              <p style={{ fontSize: 13, color: "#8080a0" }}>{r.text}</p>
                            </div>
                          </div>
                        ))}
                      </div>
                    </div>
                  );
                })}
              </div>
            )}
          </div>
        )}

        {/* ── MY PAGE ── */}
        {page === "mypage" && me && (
          <div style={{ maxWidth: 700, margin: "0 auto", padding: 24 }}>
            <div style={{ marginBottom: 32 }}>
              <div style={{ fontSize: 11, letterSpacing: 4, color: "#4040a0", marginBottom: 8 }}>MY PAGE</div>
              <h2 style={{ fontFamily: "'Noto Serif KR', serif", fontSize: 26, color: "#fff" }}>{me.nickname}</h2>
              <p style={{ color: "#4040a0", fontSize: 13, marginTop: 4 }}>수강 완료 강의 {me.completedLectures?.length || 0}개</p>
            </div>

            {/* Talents */}
            <div style={{ background: "#0d0d1e", border: "1px solid #1e1e3e", borderRadius: 16, padding: 24, marginBottom: 20 }}>
              <h3 style={{ fontFamily: "'Noto Serif KR', serif", color: "#c084fc", marginBottom: 20, fontSize: 16 }}>보유 재능 ({me.talents.length}/3)</h3>
              {me.talents.length === 0
                ? <p style={{ color: "#3a3a5e", fontSize: 14 }}>아직 개화된 재능이 없습니다. 강의를 수강해 보세요.</p>
                : <div style={{ display: "flex", gap: 16, flexWrap: "wrap" }}>
                    {me.talents.map((t, i) => {
                      const meta = CATEGORY_META[t.category] || { icon: "✦", color: "#c084fc" };
                      return (
                        <div key={i} style={{ background: "#0a0a18", border: `1px solid ${meta.color}44`, borderRadius: 12, padding: "16px 20px", minWidth: 120, textAlign: "center" }}>
                          <div style={{ fontSize: 28, marginBottom: 6 }}>{meta.icon}</div>
                          <div style={{ fontSize: 13, color: meta.color, fontWeight: 600 }}>{t.category}</div>
                          <div style={{ fontSize: 20, margin: "6px 0" }}>{TALENT_ICONS[TALENT_STAGES[t.stage]]}</div>
                          <div style={{ fontSize: 12, color: "#6060a0" }}>{TALENT_STAGES[t.stage]}</div>
                          <div style={{ marginTop: 8, display: "flex", gap: 3, justifyContent: "center" }}>
                            {[0, 1, 2].map(s => (
                              <div key={s} style={{ width: 8, height: 8, borderRadius: "50%", background: s <= t.stage ? meta.color : "#1a1a2e" }} />
                            ))}
                          </div>
                        </div>
                      );
                    })}
                  </div>
              }
            </div>

            {/* Hints received */}
            {(() => {
              const hintLectures = (me.completedLectures || [])
                .map(id => db.lectures.find(l => l.id === id))
                .filter(l => l && (l.mode || db.mode) === "hint" && l.hint);
              if (!hintLectures.length) return null;
              return (
                <div style={{ background: "#0d0d1e", border: "1px solid #fbbf2433", borderRadius: 16, padding: 24, marginBottom: 20 }}>
                  <h3 style={{ fontFamily: "'Noto Serif KR', serif", color: "#fbbf24", marginBottom: 20, fontSize: 16 }}>수신한 힌트</h3>
                  <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
                    {hintLectures.map(l => (
                      <div key={l.id} style={{ background: "#1a1500", border: "1px solid #fbbf2422", borderRadius: 10, padding: "12px 16px" }}>
                        <div style={{ fontSize: 11, color: "#fbbf2466", marginBottom: 4 }}>「{l.title}」에서 수신</div>
                        <p style={{ color: "#fbbf24", fontSize: 14, lineHeight: 1.6 }}>{l.hint}</p>
                      </div>
                    ))}
                  </div>
                </div>
              );
            })()}

            {/* Completed lectures */}
            <div style={{ background: "#0d0d1e", border: "1px solid #1e1e3e", borderRadius: 16, padding: 24 }}>
              <h3 style={{ fontFamily: "'Noto Serif KR', serif", color: "#fff", marginBottom: 16, fontSize: 16 }}>수강 이력</h3>
              {(me.completedLectures || []).length === 0
                ? <p style={{ color: "#3a3a5e", fontSize: 14 }}>수강한 강의가 없습니다.</p>
                : <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
                    {(me.completedLectures || []).map(id => {
                      const lec = db.lectures.find(l => l.id === id);
                      if (!lec) return null;
                      const meta = CATEGORY_META[lec.category] || { icon: "✦", color: "#c084fc" };
                      return (
                        <div key={id} style={{ display: "flex", alignItems: "center", gap: 12, padding: "8px 12px", background: "#0a0a18", borderRadius: 10 }}>
                          <span style={{ fontSize: 18 }}>{meta.icon}</span>
                          <div>
                            <div style={{ fontSize: 13, color: "#c0c0e0" }}>{lec.title}</div>
                            <div style={{ fontSize: 11, color: "#4040a0" }}>{lec.category} · {lec.date}</div>
                          </div>
                        </div>
                      );
                    })}
                  </div>
              }
            </div>
          </div>
        )}

        {/* ── ADMIN ── */}
        {page === "admin" && isAdmin && (
          <div style={{ maxWidth: 900, margin: "0 auto", padding: 24 }}>
            <div style={{ marginBottom: 32 }}>
              <div style={{ fontSize: 11, letterSpacing: 4, color: "#4040a0", marginBottom: 8 }}>ADMIN CONSOLE</div>
              <h2 style={{ fontFamily: "'Noto Serif KR', serif", fontSize: 26, color: "#fff" }}>관리자 패널</h2>
            </div>

            {/* Tab nav */}
            <div style={{ display: "flex", gap: 8, marginBottom: 28, background: "#0a0a18", borderRadius: 12, padding: 6, width: "fit-content" }}>
              {[["lectures", "강의 관리"], ["users", "수강생 관리"], ["settings", "시스템 설정"]].map(([k, v]) => (
                <button key={k} onClick={() => setAdminTab(k)} style={{
                  padding: "8px 20px", border: "none", borderRadius: 8, cursor: "pointer", fontFamily: "inherit", fontWeight: 600, fontSize: 13,
                  background: adminTab === k ? "#c084fc" : "transparent", color: adminTab === k ? "#fff" : "#6060a0", transition: "all 0.2s"
                }}>{v}</button>
              ))}
            </div>

            {/* LECTURES */}
            {adminTab === "lectures" && (
              <div>
                {/* Add lecture form */}
                <div style={{ background: "#0d0d1e", border: "1px solid #2a2a3e", borderRadius: 16, padding: 24, marginBottom: 24 }}>
                  <h3 style={{ color: "#c084fc", marginBottom: 16, fontFamily: "'Noto Serif KR', serif", fontSize: 16 }}>새 강의 등록</h3>
                  <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12, marginBottom: 12 }}>
                    <div>
                      <label style={{ fontSize: 11, color: "#6060a0", display: "block", marginBottom: 4 }}>강의명</label>
                      <input value={newLecture.title} onChange={e => setNewLecture(p => ({ ...p, title: e.target.value }))} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }} placeholder="강의 제목" />
                    </div>
                    <div>
                      <label style={{ fontSize: 11, color: "#6060a0", display: "block", marginBottom: 4 }}>분야</label>
                      <select value={newLecture.category} onChange={e => setNewLecture(p => ({ ...p, category: e.target.value }))} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }}>
                        {Object.keys(CATEGORY_META).map(c => <option key={c} value={c}>{c}</option>)}
                      </select>
                    </div>
                  </div>
                  <div style={{ marginBottom: 12 }}>
                    <label style={{ fontSize: 11, color: "#6060a0", display: "block", marginBottom: 4 }}>강의 설명</label>
                    <textarea value={newLecture.desc} onChange={e => setNewLecture(p => ({ ...p, desc: e.target.value }))} rows={2} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14, resize: "none" }} placeholder="강의 설명" />
                  </div>
                  <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12, marginBottom: 16 }}>
                    <div>
                      <label style={{ fontSize: 11, color: "#6060a0", display: "block", marginBottom: 4 }}>수강 후 발급 모드</label>
                      <select value={newLecture.mode} onChange={e => setNewLecture(p => ({ ...p, mode: e.target.value }))} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }}>
                        <option value="talent">재능 발급</option>
                        <option value="hint">힌트 발급</option>
                      </select>
                    </div>
                    {newLecture.mode === "hint" && (
                      <div>
                        <label style={{ fontSize: 11, color: "#6060a0", display: "block", marginBottom: 4 }}>힌트 문구</label>
                        <input value={newLecture.hint} onChange={e => setNewLecture(p => ({ ...p, hint: e.target.value }))} style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14 }} placeholder="수강 완료 시 표시될 힌트" />
                      </div>
                    )}
                  </div>
                  <button onClick={addLecture} style={btnStyle("#c084fc")}>강의 등록</button>
                </div>

                {/* Lecture list */}
                <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
                  {db.lectures.length === 0
                    ? <p style={{ color: "#3a3a5e", fontSize: 14 }}>등록된 강의가 없습니다.</p>
                    : db.lectures.map(lec => {
                        const meta = CATEGORY_META[lec.category] || { icon: "✦", color: "#c084fc" };
                        const effectiveMode = lec.mode || db.mode;
                        return (
                          <div key={lec.id} style={{ background: "#0d0d1e", border: "1px solid #1e1e3e", borderRadius: 12, padding: "14px 18px", display: "flex", alignItems: "center", gap: 12 }}>
                            <span style={{ fontSize: 20 }}>{meta.icon}</span>
                            <div style={{ flex: 1 }}>
                              <div style={{ display: "flex", gap: 8, alignItems: "center", marginBottom: 4 }}>
                                <span style={{ fontSize: 14, color: "#c0c0e0", fontWeight: 600 }}>{lec.title}</span>
                                <span style={{ fontSize: 11, color: meta.color, background: meta.color + "22", borderRadius: 4, padding: "1px 6px" }}>{lec.category}</span>
                                <span style={{ fontSize: 11, color: effectiveMode === "hint" ? "#fbbf24" : "#c084fc", background: effectiveMode === "hint" ? "#fbbf2422" : "#c084fc22", borderRadius: 4, padding: "1px 6px" }}>{effectiveMode === "hint" ? "힌트" : "재능"}</span>
                              </div>
                              <div style={{ fontSize: 12, color: "#4040a0" }}>{lec.date} · 수강 {lec.enrolled.length}/{lec.slots} · 후기 {(db.reviews[lec.id] || []).length}개</div>
                            </div>
                            <button onClick={() => deleteLecture(lec.id)} style={btnStyle("#f8717144", true)}>삭제</button>
                          </div>
                        );
                      })
                  }
                </div>
              </div>
            )}

            {/* USERS */}
            {adminTab === "users" && (
              <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
                {Object.values(db.users).filter(u => u.id !== "admin").map(u => (
                  <div key={u.uid} style={{ background: "#0d0d1e", border: "1px solid #1e1e3e", borderRadius: 12, padding: "14px 18px" }}>
                    <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start" }}>
                      <div>
                        <div style={{ fontSize: 14, color: "#c0c0e0", fontWeight: 600 }}>{u.nickname} <span style={{ color: "#4040a0", fontWeight: 400 }}>@{u.id}</span></div>
                        <div style={{ fontSize: 12, color: "#4040a0", marginTop: 4 }}>수강 완료 {u.completedLectures?.length || 0}개 · 재능 {u.talents?.length || 0}/3</div>
                      </div>
                      <div style={{ display: "flex", gap: 6 }}>
                        {u.talents?.map((t, i) => {
                          const meta = CATEGORY_META[t.category] || { icon: "✦", color: "#c084fc" };
                          return <span key={i} style={{ fontSize: 13, color: meta.color }}>{meta.icon} {t.category} ({TALENT_STAGES[t.stage]})</span>;
                        })}
                      </div>
                    </div>
                  </div>
                ))}
                {Object.values(db.users).filter(u => u.id !== "admin").length === 0 && (
                  <p style={{ color: "#3a3a5e", fontSize: 14 }}>등록된 수강생이 없습니다.</p>
                )}
              </div>
            )}

            {/* SETTINGS */}
            {adminTab === "settings" && (
              <div style={{ background: "#0d0d1e", border: "1px solid #2a2a3e", borderRadius: 16, padding: 28 }}>
                <h3 style={{ color: "#c084fc", marginBottom: 24, fontFamily: "'Noto Serif KR', serif", fontSize: 16 }}>전체 모드 설정</h3>
                <p style={{ color: "#6060a0", fontSize: 13, marginBottom: 20, lineHeight: 1.7 }}>
                  강의별로 모드가 지정되지 않은 경우 이 설정이 기본값으로 적용됩니다.<br />
                  현재 기본 모드: <span style={{ color: globalMode === "hint" ? "#fbbf24" : "#c084fc", fontWeight: 700 }}>{globalMode === "hint" ? "힌트 발급" : "재능 발급"}</span>
                </p>
                <div style={{ display: "flex", gap: 12 }}>
                  <button onClick={() => changeGlobalMode("talent")} style={{ ...btnStyle(globalMode === "talent" ? "#c084fc" : "#2a2a3e"), padding: "12px 24px" }}>
                    🌸 재능 발급 모드
                  </button>
                  <button onClick={() => changeGlobalMode("hint")} style={{ ...btnStyle(globalMode === "hint" ? "#fbbf24" : "#2a2a3e"), color: globalMode === "hint" ? "#000" : "#fff", padding: "12px 24px" }}>
                    💡 힌트 발급 모드
                  </button>
                </div>
              </div>
            )}
          </div>
        )}
      </div>

      {/* ── MINI GAME MODAL ── */}
      {gamePhase === "playing" && selectedLecture && (
        <Modal onClose={() => { setGamePhase(null); setSelectedLecture(null); }}>
          <div style={{ fontSize: 11, letterSpacing: 3, color: "#4040a0", marginBottom: 8 }}>수련 과정</div>
          <h3 style={{ fontFamily: "'Noto Serif KR', serif", color: "#fff", marginBottom: 4 }}>{selectedLecture.title}</h3>
          <p style={{ fontSize: 12, color: "#4040a0", marginBottom: 20 }}>미니게임을 클리어하면 수강이 완료됩니다.</p>
          <MiniGame onComplete={onGameComplete} />
        </Modal>
      )}

      {/* ── REVIEW MODAL ── */}
      {gamePhase === "review" && selectedLecture && (
        <Modal onClose={() => { setGamePhase(null); setSelectedLecture(null); }}>
          {(() => {
            const lec = selectedLecture;
            const effectiveMode = lec.mode || db.mode;
            return (
              <>
                <div style={{ textAlign: "center", marginBottom: 20 }}>
                  <div style={{ fontSize: 40, marginBottom: 8 }}>{effectiveMode === "hint" ? "💡" : "🌸"}</div>
                  <h3 style={{ fontFamily: "'Noto Serif KR', serif", color: effectiveMode === "hint" ? "#fbbf24" : "#c084fc", marginBottom: 8 }}>
                    {effectiveMode === "hint" ? "힌트를 수신했습니다" : "재능이 개화했습니다"}
                  </h3>
                  {effectiveMode === "hint" && lec.hint
                    ? <div style={{ background: "#1a1500", border: "1px solid #fbbf2433", borderRadius: 10, padding: "14px 18px", margin: "12px 0", color: "#fbbf24", fontSize: 14, lineHeight: 1.7 }}>{lec.hint}</div>
                    : <p style={{ color: "#6060a0", fontSize: 13 }}>
                        {lec.category} 재능이 성장했습니다. 마이페이지에서 확인해 보세요.
                      </p>
                  }
                </div>
                <div style={{ borderTop: "1px solid #1a1a2e", paddingTop: 20, marginTop: 8 }}>
                  <div style={{ fontSize: 13, color: "#6060a0", marginBottom: 12 }}>강의 후기를 남겨 주세요</div>
                  <div style={{ marginBottom: 12 }}>
                    <StarRating value={reviewForm.star} onChange={s => setReviewForm(p => ({ ...p, star: s }))} />
                  </div>
                  <textarea
                    value={reviewForm.text}
                    onChange={e => setReviewForm(p => ({ ...p, text: e.target.value }))}
                    rows={3}
                    placeholder="한 줄 후기를 입력해 주세요..."
                    style={{ width: "100%", background: "#1a1a2e", border: "1px solid #2a2a4e", color: "#fff", borderRadius: 8, padding: "10px 14px", fontSize: 14, resize: "none", fontFamily: "inherit" }}
                  />
                  <div style={{ display: "flex", gap: 10, marginTop: 14 }}>
                    <button onClick={submitReview} style={{ ...btnStyle("#c084fc"), flex: 1 }}>후기 제출 및 완료</button>
                    <button onClick={() => { setGamePhase(null); setSelectedLecture(null); showToast("수강 완료!"); }} style={{ ...btnStyle("#2a2a3e"), flex: 0, whiteSpace: "nowrap" }}>건너뛰기</button>
                  </div>
                </div>
              </>
            );
          })()}
        </Modal>
      )}
    </div>
  );
}
