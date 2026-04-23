import React, { useState, useEffect } from 'react';
import { 
  BookOpen, 
  Compass, 
  Grid3X3, 
  PlusSquare, 
  Orbit, 
  MapPin, 
  ArrowDownToLine, 
  Globe, 
  Menu, 
  X,
  ChevronRight,
  Lightbulb,
  Info,
  Rocket,
  Target,
  CheckCircle2,
  PlaySquare,
  Calculator,
  Gamepad,
  Camera,
  Navigation,
  Wind,
  Cpu,
  Building2,
  Ship
} from 'lucide-react';

// --- Reusable UI Components ---

const Formula = ({ main, note, color = "indigo" }) => {
  const colors = {
    indigo: "bg-indigo-50 border-indigo-200 text-indigo-900",
    emerald: "bg-emerald-50 border-emerald-200 text-emerald-900",
    amber: "bg-amber-50 border-amber-200 text-amber-900",
    rose: "bg-rose-50 border-rose-200 text-rose-900",
  };
  
  return (
    <div className={`border-2 rounded-2xl p-5 my-4 ${colors[color]} shadow-sm`}>
      <div className="font-serif text-xl font-black text-center tracking-wide overflow-x-auto whitespace-nowrap pb-2 scrollbar-hide">
        {main}
      </div>
      {note && <div className="text-xs font-semibold text-center mt-3 opacity-80 border-t border-current pt-2">{note}</div>}
    </div>
  );
};

const Callout = ({ title, children, icon: Icon, color = "blue" }) => {
  const colors = {
    blue: "bg-blue-50 border-blue-200 text-blue-800",
    amber: "bg-amber-50 border-amber-200 text-amber-800",
    purple: "bg-purple-50 border-purple-200 text-purple-800",
    rose: "bg-rose-50 border-rose-200 text-rose-800",
    emerald: "bg-emerald-50 border-emerald-200 text-emerald-800",
  };
  
  const iconColors = {
    blue: "text-blue-600 bg-blue-100",
    amber: "text-amber-600 bg-amber-100",
    purple: "text-purple-600 bg-purple-100",
    rose: "text-rose-600 bg-rose-100",
    emerald: "text-emerald-600 bg-emerald-100",
  };
  
  return (
    <div className={`border-2 rounded-2xl p-4 my-6 flex gap-3 items-start ${colors[color]} shadow-sm`}>
      <div className={`p-2 rounded-xl ${iconColors[color]} shrink-0 mt-0.5`}>
        <Icon size={20} />
      </div>
      <div>
        <h4 className="font-bold text-base mb-1.5 leading-tight">{title}</h4>
        <div className="text-sm opacity-90 leading-relaxed space-y-2">{children}</div>
      </div>
    </div>
  );
};

const ExampleBox = ({ question, answerSteps, customTitle }) => {
  const [isOpen, setIsOpen] = useState(false);
  
  return (
    <div className="bg-white border-2 border-slate-200 rounded-2xl overflow-hidden my-6 shadow-sm">
      <div className="p-4 bg-slate-50 border-b border-slate-200 flex flex-col gap-3">
        <div className="bg-indigo-100 text-indigo-700 font-black px-3 py-1.5 rounded-lg text-xs w-max flex items-center gap-1.5 tracking-wider">
          <Target size={14} /> {customTitle || "CONTOH SOAL"}
        </div>
        <div className="font-medium text-slate-800 text-sm leading-relaxed">{question}</div>
      </div>
      
      {isOpen ? (
        <div className="p-4 bg-indigo-50/60 animate-in fade-in slide-in-from-top-2 duration-300">
          <div className="flex items-center gap-2 text-sm font-bold text-indigo-800 mb-4 border-b border-indigo-200 pb-2">
            <CheckCircle2 size={16} /> Pembahasan:
          </div>
          <div className="space-y-3 text-slate-700 text-sm leading-relaxed">
            {answerSteps}
          </div>
          <button 
            onClick={() => setIsOpen(false)} 
            className="mt-6 px-4 py-2.5 bg-slate-200 hover:bg-slate-300 text-slate-700 text-sm font-bold rounded-xl transition-colors w-full flex justify-center items-center gap-2 active:scale-[0.98]"
          >
            Tutup Pembahasan
          </button>
        </div>
      ) : (
        <div className="p-2 bg-white text-center hover:bg-slate-50 transition-colors cursor-pointer active:bg-slate-100" onClick={() => setIsOpen(true)}>
          <button className="text-sm font-bold text-indigo-600 transition-colors flex items-center justify-center gap-2 w-full py-2">
            <PlaySquare size={18} /> Lihat Jawaban Lengkap
          </button>
        </div>
      )}
    </div>
  );
};

const MathVar = ({ children }) => <span className="font-serif italic font-bold mx-0.5 text-indigo-700">{children}</span>;
const Vec = ({ children }) => <span className="font-bold mx-0.5 text-indigo-800">{children}</span>;

const HeroImage = ({ src, alt, caption }) => (
  <div className="mb-6 rounded-2xl overflow-hidden shadow-sm border border-slate-200 relative">
    <div className="relative h-48 sm:h-64 overflow-hidden bg-slate-200">
      <img src={src} alt={alt} className="w-full h-full object-cover" loading="lazy" />
      <div className="absolute inset-0 bg-gradient-to-t from-slate-900/90 via-slate-900/30 to-transparent"></div>
      <div className="absolute bottom-3 left-3 right-3 text-white text-xs sm:text-sm font-medium leading-snug flex items-start gap-2">
        <Info size={16} className="shrink-0 text-indigo-300 mt-0.5" />
        <p>{caption}</p>
      </div>
    </div>
  </div>
);

// --- Section Content Components ---

const Definisi = () => (
  <div className="space-y-6 animate-in fade-in duration-500">
    <div className="mb-4">
      <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">1. Vektor & Skalar 👋</h2>
      <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">Apa sih bedanya besaran yang dipelajari di SMP sama besaran Vektor? Intinya ada di kata <b>"Arah"</b>!</p>
    </div>

    <HeroImage 
      src="https://images.unsplash.com/photo-1469854523086-cc02fe5d8800?auto=format&fit=crop&w=800&q=80" 
      alt="Mobil melaju di jalan raya"
      caption="Speedometer mobil menunjukkan 80 km/jam (Skalar). Tapi GPS menunjukkan 80 km/jam bergerak menuju Utara (Vektor)."
    />

    <div className="flex flex-col gap-4">
      <div className="border-l-4 border-indigo-500 bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
        <div className="flex items-center gap-3 mb-3">
          <div className="p-2 bg-indigo-100 text-indigo-600 rounded-xl"><Compass size={18} /></div>
          <h3 className="font-extrabold text-lg text-indigo-900">Besaran Vektor 🎯</h3>
        </div>
        <p className="text-slate-600 text-sm leading-relaxed mb-3">
          Wajib memiliki <span className="font-bold text-indigo-600 bg-indigo-50 px-1 rounded">Nilai</span> dan <span className="font-bold text-indigo-600 bg-indigo-50 px-1 rounded">Arah</span>. Informasi tidak lengkap tanpa arah.
        </p>
        <div className="bg-indigo-50/50 p-3 rounded-xl border border-indigo-100">
          <div className="text-xs font-bold text-indigo-800 mb-1">Contoh Nyata:</div>
          <ul className="space-y-1.5 text-sm text-indigo-700 font-medium ml-1">
            <li>🚀 <b>Kecepatan:</b> Melaju 100 km/jam ke Timur.</li>
            <li>📍 <b>Perpindahan:</b> Pindah 5 meter ke Kanan.</li>
            <li>💪 <b>Gaya:</b> Dorong meja 50 N ke Depan.</li>
          </ul>
        </div>
      </div>

      <div className="border-l-4 border-emerald-500 bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
        <div className="flex items-center gap-3 mb-3">
          <div className="p-2 bg-emerald-100 text-emerald-600 rounded-xl"><Orbit size={18} /></div>
          <h3 className="font-extrabold text-lg text-emerald-900">Besaran Skalar ⚖️</h3>
        </div>
        <p className="text-slate-600 text-sm leading-relaxed mb-3">
          Hanya butuh <span className="font-bold text-emerald-600 bg-emerald-50 px-1 rounded">Nilai (Angka)</span>. Arah sama sekali tidak mempengaruhi kejelasan infonya.
        </p>
        <div className="bg-emerald-50/50 p-3 rounded-xl border border-emerald-100">
          <div className="text-xs font-bold text-emerald-800 mb-1">Contoh Nyata:</div>
          <ul className="space-y-1.5 text-sm text-emerald-700 font-medium ml-1">
            <li>🌡️ <b>Suhu:</b> Hari ini 30°C.</li>
            <li>⏱️ <b>Waktu:</b> Ujian sisa 90 menit.</li>
            <li>⚖️ <b>Massa:</b> Beras ini beratnya 5 Kg.</li>
          </ul>
        </div>
      </div>
    </div>

    <Callout title="Cara Penulisan Vektor" icon={BookOpen} color="amber">
      <p>Dalam matematika, penulisan vektor itu spesial untuk membedakannya dengan angka biasa:</p>
      <div className="flex flex-col sm:flex-row gap-3 mt-3">
        <div className="bg-white p-3 rounded-xl border border-amber-200 flex-1 text-center">
          <div className="font-serif font-black text-xl mb-1 text-amber-900">F atau v</div>
          <div className="text-xs">Di buku cetak dicetak <b>Tebal (Bold)</b>.</div>
        </div>
        <div className="bg-white p-3 rounded-xl border border-amber-200 flex-1 text-center">
          <div className="relative text-xl font-serif font-bold text-amber-900 mb-1">
             <span className="absolute -top-3 left-0 right-0 text-center text-sm">→</span>
             F
          </div>
          <div className="text-xs">Diberi <b>tanda panah</b> saat ditulis tangan.</div>
        </div>
      </div>
    </Callout>

    <ExampleBox 
      question={<>Budi berjalan 4 meter ke arah Timur, lalu berbelok 3 meter ke arah Utara. <br/><br/><b>Hitung Jarak (Skalar) dan Perpindahannya (Vektor)!</b></>}
      answerSteps={
        <>
          <p><b>1. Jarak (Sifatnya Skalar)</b></p>
          <p>Jarak itu total tempuh, ibaratnya menghitung jumlah kalori yang terbakar. Tinggal tambahin semua perjalanannya, nggak peduli belok ke mana.</p>
          <div className="bg-white p-3 rounded-xl border border-slate-200 font-mono text-sm shadow-sm text-center">
            Jarak = 4m + 3m = <b>7 meter</b>
          </div>
          
          <div className="border-t border-slate-200 my-4"></div>
          
          <p><b>2. Perpindahan (Sifatnya Vektor)</b></p>
          <p>Perpindahan sangat peduli arah! Menghitungnya adalah menarik garis lurus dari <b>titik awal (Start) ke titik akhir (Finish)</b>.</p>
          <p>Karena Timur dan Utara membentuk sudut siku-siku (90°), kita gunakan rumus Pythagoras!</p>
          <div className="bg-white p-3 rounded-xl border border-slate-200 font-mono text-sm shadow-sm overflow-x-auto whitespace-nowrap">
            Perpindahan = &radic;(4² + 3²) <br/>
            Perpindahan = &radic;(16 + 9) <br/>
            Perpindahan = &radic;25 = <b>5 meter (arah Serong/Timur Laut)</b>
          </div>
          <div className="mt-2 text-xs text-indigo-700 bg-indigo-100/50 p-2 rounded-lg font-bold">
            💡 Kesimpulan: Nilai Skalar (7m) dan Vektor (5m) bisa berbeda walau kasusnya sama!
          </div>
        </>
      }
    />
  </div>
);

const Geometris = () => {
  const [activeTab, setActiveTab] = useState('segitiga');

  return (
    <div className="space-y-6 animate-in fade-in duration-500">
      <div className="mb-4">
        <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">2. Vektor Geometris 🏹</h2>
        <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">Secara visual, vektor digambarkan sebagai anak panah. Panjang panah mewakili Nilai, dan Ujung panah mewakili Arah.</p>
      </div>

      <div className="bg-slate-900 border border-slate-800 rounded-3xl text-white overflow-hidden shadow-lg">
        <div className="p-5 sm:p-6 relative z-10">
          <h3 className="font-bold text-xl mb-2 flex items-center gap-2 text-emerald-400">
            <Gamepad size={22} /> Simulator Geometri
          </h3>
          <p className="text-slate-300 mb-5 text-sm leading-relaxed">
            Konsep penjumlahan vektor paling dasar: <b>Pangkal Ketemu Ujung!</b><br/>
            Bayangkan jalan dari titik A ke B (<span className="text-indigo-400 font-bold">Vektor a</span>), lalu lanjut dari B ke C (<span className="text-emerald-400 font-bold">Vektor b</span>). Jalan pintas langsung dari A ke C itulah <b>Resultannya</b>!
          </p>

          <div className="flex flex-col sm:flex-row gap-2 bg-slate-800 p-1.5 rounded-xl mb-6">
            <button 
              onClick={() => setActiveTab('segitiga')}
              className={`flex-1 py-2.5 px-4 text-sm font-bold rounded-lg transition-all text-center ${activeTab === 'segitiga' ? 'bg-indigo-500 text-white shadow-md' : 'text-slate-400 hover:text-white active:bg-slate-700'}`}
            >
              Metode Segitiga
            </button>
            <button 
              onClick={() => setActiveTab('jajargenjang')}
              className={`flex-1 py-2.5 px-4 text-sm font-bold rounded-lg transition-all text-center ${activeTab === 'jajargenjang' ? 'bg-emerald-500 text-white shadow-md' : 'text-slate-400 hover:text-white active:bg-slate-700'}`}
            >
              Metode Jajargenjang
            </button>
          </div>

          <div className="bg-slate-950 p-4 rounded-2xl flex justify-center items-center min-h-[220px] relative overflow-hidden border border-slate-800/50 shadow-inner">
            {activeTab === 'segitiga' ? (
              <svg viewBox="0 0 200 130" className="w-full max-w-[300px] animate-in zoom-in-95 duration-300">
                <defs>
                  <marker id="arr-a" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#818cf8"/></marker>
                  <marker id="arr-b" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#34d399"/></marker>
                  <marker id="arr-r" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#fb7185"/></marker>
                </defs>
                {/* Vector a */}
                <line x1="30" y1="100" x2="110" y2="40" stroke="#818cf8" strokeWidth="4" markerEnd="url(#arr-a)"/>
                {/* Vector b (Head to tail) */}
                <line x1="110" y1="40" x2="170" y2="80" stroke="#34d399" strokeWidth="4" markerEnd="url(#arr-b)"/>
                
                {/* Animated Resultant Line */}
                <line x1="30" y1="100" x2="168" y2="80" stroke="#fb7185" strokeWidth="4.5" strokeDasharray="6,4" markerEnd="url(#arr-r)">
                   <animate attributeName="stroke-dashoffset" values="40;0" dur="1.5s" repeatCount="indefinite"/>
                </line>
                
                <text x="50" y="60" fontSize="13" fill="#818cf8" fontWeight="bold">a (Langkah 1)</text>
                <text x="140" y="50" fontSize="13" fill="#34d399" fontWeight="bold">b (Langkah 2)</text>
                <text x="50" y="115" fontSize="13" fill="#fb7185" fontWeight="bold">a + b (Jalan Pintas!)</text>
                
                <circle cx="30" cy="100" r="5" fill="#f8fafc"/>
                <circle cx="170" cy="80" r="5" fill="#f8fafc"/>
              </svg>
            ) : (
              <svg viewBox="0 0 200 130" className="w-full max-w-[300px] animate-in zoom-in-95 duration-300">
                <defs>
                  <marker id="arr-a2" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#818cf8"/></marker>
                  <marker id="arr-b2" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#34d399"/></marker>
                  <marker id="arr-r2" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#fb7185"/></marker>
                </defs>
                {/* Vector a and b (Tail to tail) */}
                <line x1="40" y1="100" x2="120" y2="40" stroke="#818cf8" strokeWidth="4" markerEnd="url(#arr-a2)"/>
                <line x1="40" y1="100" x2="100" y2="100" stroke="#34d399" strokeWidth="4" markerEnd="url(#arr-b2)"/>
                
                {/* Parallelogram helper lines */}
                <line x1="120" y1="40" x2="180" y2="40" stroke="#34d399" strokeWidth="2" strokeDasharray="4,4" opacity="0.4"/>
                <line x1="100" y1="100" x2="180" y2="40" stroke="#818cf8" strokeWidth="2" strokeDasharray="4,4" opacity="0.4"/>
                
                {/* Resultant */}
                <line x1="40" y1="100" x2="178" y2="41" stroke="#fb7185" strokeWidth="4.5" strokeDasharray="6,4" markerEnd="url(#arr-r2)">
                  <animate attributeName="stroke-dashoffset" values="40;0" dur="1.5s" repeatCount="indefinite"/>
                </line>

                <text x="50" y="60" fontSize="13" fill="#818cf8" fontWeight="bold">Gaya 1 (a)</text>
                <text x="60" y="120" fontSize="13" fill="#34d399" fontWeight="bold">Gaya 2 (b)</text>
                <text x="120" y="85" fontSize="13" fill="#fb7185" fontWeight="bold">Resultan Gabungan</text>
                <circle cx="40" cy="100" r="5" fill="#f8fafc"/>
              </svg>
            )}
          </div>
          
          <div className="mt-4 flex gap-3 text-xs sm:text-sm text-slate-300 bg-slate-800/80 p-3 sm:p-4 rounded-xl border border-slate-700 leading-relaxed">
            <span className="text-xl">💡</span> 
            <p><b>Tips:</b> Metode Segitiga cocok untuk kasus perpindahan berantai. Sedangkan Jajargenjang cocok untuk melihat dua gaya tarikan yang berpusat di titik yang sama.</p>
          </div>
        </div>
      </div>

      <ExampleBox 
        question={<>Diberikan panah vektor <Vec>p</Vec> menghadap ke "Serong Kanan-Atas" dan panah vektor <Vec>q</Vec> menghadap ke "Kanan".<br/><br/>Bagaimana cara menggambar resultan pengurangan vektor <b><Vec>p</Vec> - <Vec>q</Vec></b> ?</>}
        answerSteps={
          <>
            <p>Pengurangan vektor secara geometris sejatinya adalah <b>penjumlahan dengan vektor yang arahnya dibalik (vektor negatif)</b>.</p>
            <div className="bg-slate-100 p-3 rounded-lg border border-slate-200 font-mono text-xs sm:text-sm text-center font-bold">
              <Vec>p</Vec> - <Vec>q</Vec>  =  <Vec>p</Vec> + (-<Vec>q</Vec>)
            </div>
            <ol className="list-decimal pl-5 space-y-2.5 mt-3">
              <li>Gambar vektor <Vec>p</Vec> normal (menghadap Kanan-Atas).</li>
              <li>Buat vektor negatif <Vec>q</Vec>. Karena <Vec>q</Vec> awal menghadap ke Kanan, maka <b>-<Vec>q</Vec> harus menghadap ke Kiri</b> sejajar.</li>
              <li>Pindahkan (geser) panah -<Vec>q</Vec> tersebut sehingga pangkalnya menempel tepat di ujung panah <Vec>p</Vec>.</li>
              <li>Tarik garis lurus dari pangkal awal <Vec>p</Vec> menuju ujung panah -<Vec>q</Vec> yang baru. Selesai! Garis itu adalah Resultannya.</li>
            </ol>
          </>
        }
      />
    </div>
  );
};

const Analitik = () => {
  const [x, setX] = useState(4);
  const [y, setY] = useState(3);
  
  const length = Math.sqrt(x*x + y*y).toFixed(2);

  return (
    <div className="space-y-6 animate-in fade-in duration-500">
      <div className="mb-4">
        <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">3. Koordinat Analitik 🎮</h2>
        <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">Menggambar panah terus-terusan itu capek. Makanya, vektor "diterjemahkan" ke dalam bentuk angka koordinat (x, y, z) supaya bisa dihitung otomatis!</p>
      </div>

      <div className="bg-white border border-slate-200 rounded-3xl p-5 sm:p-6 shadow-sm">
        <h3 className="font-bold text-lg mb-4 text-slate-800">Menulis Vektor dalam Sumbu</h3>
        <p className="text-slate-600 mb-5 text-sm leading-relaxed">
          Panah miring dipecah jadi 2 komponen: Seberapa jauh dia jalan di sumbu mendatar (X) dan sumbu tegak (Y). 
          Ada yang namanya <b>Vektor Basis</b> sebagai penunjuk arah sumbu: <Vec>i</Vec> untuk X, <Vec>j</Vec> untuk Y, dan <Vec>k</Vec> untuk Z.
        </p>
        
        <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
          <div className="bg-slate-50 border border-slate-200 rounded-2xl p-4 hover:border-indigo-300 transition-colors">
            <div className="font-bold text-indigo-600 mb-2 text-xs uppercase tracking-wider">Di Bidang Datar (2D)</div>
            <div className="font-serif font-black text-indigo-900 text-lg sm:text-xl overflow-x-auto whitespace-nowrap scrollbar-hide">
              <Vec>v</Vec> = x<Vec>i</Vec> + y<Vec>j</Vec> = <span className="text-indigo-600">(x, y)</span>
            </div>
            <div className="text-xs text-slate-500 mt-2">Seperti koordinat game Mario Bros (maju & lompat).</div>
          </div>
          <div className="bg-slate-50 border border-slate-200 rounded-2xl p-4 hover:border-emerald-300 transition-colors">
            <div className="font-bold text-emerald-600 mb-2 text-xs uppercase tracking-wider">Di Ruang Nyata (3D)</div>
            <div className="font-serif font-black text-emerald-900 text-lg sm:text-xl overflow-x-auto whitespace-nowrap scrollbar-hide">
              <Vec>v</Vec> = x<Vec>i</Vec> + y<Vec>j</Vec> + z<Vec>k</Vec> = <span className="text-emerald-600">(x, y, z)</span>
            </div>
            <div className="text-xs text-slate-500 mt-2">Seperti dunia 3D FreeFire / Roblox (segala arah).</div>
          </div>
        </div>
      </div>

      {/* Mobile-Optimized Grid Simulation Card */}
      <div className="bg-white border border-slate-200 rounded-3xl p-5 shadow-sm overflow-hidden flex flex-col">
        <div className="flex items-center gap-2 mb-2">
          <Grid3X3 className="text-indigo-500" size={20}/>
          <h3 className="font-bold text-lg text-slate-800">Simulator Koordinat</h3>
        </div>
        <p className="text-xs text-slate-500 mb-5">Geser slider untuk memecah vektor merah menjadi komponen X dan Y-nya.</p>
        
        <div className="flex-1 bg-[url('https://www.transparenttextures.com/patterns/graphy.png')] bg-blue-50/50 border border-blue-200 rounded-2xl p-4 flex flex-col gap-6">
          <div className="w-full aspect-square max-w-[220px] mx-auto bg-white border border-blue-200 rounded-xl shadow-sm overflow-hidden p-1 relative">
            <svg viewBox="-1 -1 12 12" className="w-full h-full transform scale-y-[-1]">
              {[...Array(11)].map((_, i) => (
                <g key={i}>
                  <line x1={i} y1="0" x2={i} y2="10" stroke="#cbd5e1" strokeWidth="0.1" />
                  <line x1="0" y1={i} x2="10" y2={i} stroke="#cbd5e1" strokeWidth="0.1" />
                </g>
              ))}
              <line x1="0" y1="0" x2="11" y2="0" stroke="#334155" strokeWidth="0.3" markerEnd="url(#arrow)" />
              <line x1="0" y1="0" x2="0" y2="11" stroke="#334155" strokeWidth="0.3" markerEnd="url(#arrow)" />
              
              <line x1="0" y1="0" x2={x} y2="0" stroke="#818cf8" strokeWidth="0.5" strokeDasharray="0.5,0.5" />
              <line x1={x} y1="0" x2={x} y2={y} stroke="#34d399" strokeWidth="0.5" strokeDasharray="0.5,0.5" />
              
              <defs>
                <marker id="arrow-vec" markerWidth="3" markerHeight="3" refX="2.5" refY="1.5" orient="auto"><path d="M0,0 L0,3 L3,1.5 z" fill="#ef4444"/></marker>
              </defs>
              <line x1="0" y1="0" x2={x} y2={y} stroke="#ef4444" strokeWidth="0.5" markerEnd="url(#arrow-vec)">
                  <animate attributeName="x2" values={`0;${x}`} dur="0.3s" />
                  <animate attributeName="y2" values={`0;${y}`} dur="0.3s" />
              </line>
              <circle cx={x} cy={y} r="0.3" fill="#ef4444" />
            </svg>
          </div>

          <div className="space-y-4">
            <div className="bg-white/80 p-3 rounded-xl border border-indigo-100 shadow-sm">
              <div className="flex justify-between items-center mb-2">
                <span className="text-xs font-bold text-indigo-700">Komponen X (Mendatar)</span>
                <span className="font-mono font-bold bg-indigo-100 text-indigo-700 px-2 rounded">{x}</span>
              </div>
              <input type="range" min="1" max="10" value={x} onChange={(e) => setX(parseInt(e.target.value))} className="w-full accent-indigo-500 h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer" />
            </div>
            
            <div className="bg-white/80 p-3 rounded-xl border border-emerald-100 shadow-sm">
              <div className="flex justify-between items-center mb-2">
                <span className="text-xs font-bold text-emerald-700">Komponen Y (Tegak)</span>
                <span className="font-mono font-bold bg-emerald-100 text-emerald-700 px-2 rounded">{y}</span>
              </div>
              <input type="range" min="1" max="10" value={y} onChange={(e) => setY(parseInt(e.target.value))} className="w-full accent-emerald-500 h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer" />
            </div>

            <div className="bg-slate-800 p-3 rounded-xl text-center shadow-md">
              <div className="text-xs text-slate-400 mb-1">Panjang Vektor (Pythagoras):</div>
              <div className="text-sm font-mono text-slate-200">
                &radic;({x}² + {y}²) = <span className="font-black text-rose-400 text-lg ml-1">{length}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <ExampleBox 
        question={<>Titik awal A berada di kordinat (1, 2, 3) dan titik ujung B di koordinat (4, -2, 5). <br/><br/>Tentukan <b>vektor posisi <Vec>AB</Vec></b> dan <b>hitung panjang vektor tersebut!</b></>}
        answerSteps={
          <>
            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">A. Mencari Vektor AB</p>
            <p>Vektor yang menghubungkan 2 titik gampang dicari: <b>Titik Akhir (Tujuan) dikurangi Titik Awal.</b></p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto">
              <Vec>AB</Vec> = B - A <br/>
              <Vec>AB</Vec> = (4, -2, 5) - (1, 2, 3) <br/>
              <span className="text-slate-400">// kurangi X dgn X, Y dgn Y, dst</span><br/>
              <Vec>AB</Vec> = (4-1, -2-2, 5-3) <br/>
              <Vec>AB</Vec> = <b className="text-indigo-600">(3, -4, 2)</b>
            </div>
            
            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2 mt-4">B. Menghitung Panjang Vektor |AB|</p>
            <p>Panjang dihitung murni pakai Theorema Pythagoras. Kuadratkan semua angkanya, jumlahkan, lalu diakar!</p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto">
              |<Vec>AB</Vec>| = &radic;( 3² + (-4)² + 2² ) <br/>
              |<Vec>AB</Vec>| = &radic;( 9 + 16 + 4 ) <br/>
              |<Vec>AB</Vec>| = <b className="text-rose-600">&radic;29</b>
            </div>
          </>
        }
      />
    </div>
  );
};

const Operasi = () => {
  const [vX, setVX] = useState(3);
  const [vY, setVY] = useState(2);
  const [scalar, setScalar] = useState(-1);

  return (
    <div className="space-y-6 animate-in fade-in duration-500">
      <div className="mb-4">
        <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">4. Aljabar Vektor 🧮</h2>
        <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">Berhitung dengan vektor dalam wujud angka (koordinat) itu gampang banget. Aturan utamanya: <b>Operasikan komponen yang sejenis!</b></p>
      </div>

      <div className="flex flex-col gap-4">
        <div className="bg-white border-2 border-indigo-100 rounded-3xl p-5 shadow-sm">
           <div className="flex items-center gap-2 mb-3">
             <Calculator className="text-indigo-600" size={20}/>
             <h3 className="font-bold text-lg text-slate-800">Penjumlahan / Pengurangan</h3>
           </div>
           <p className="text-sm text-slate-600 mb-3">Tinggal sejajarkan. Tambah/Kurang X dengan X, Y dengan Y.</p>
           <div className="bg-indigo-50 p-3 rounded-xl border border-indigo-200 text-center font-serif font-black text-indigo-900 text-sm sm:text-base overflow-x-auto">
             (x₁, y₁) + (x₂, y₂) = (x₁ + x₂, y₁ + y₂)
           </div>
        </div>
        
        <div className="bg-white border-2 border-emerald-100 rounded-3xl p-5 shadow-sm">
           <div className="flex items-center gap-2 mb-3">
             <PlusSquare className="text-emerald-600" size={20}/>
             <h3 className="font-bold text-lg text-slate-800">Perkalian Skalar (K)</h3>
           </div>
           <p className="text-sm text-slate-600 mb-3">Skalar adalah angka biasa pencipta "efek Zoom". Angka ini dikalikan masuk ke setiap komponen di dalam kurung.</p>
           <div className="bg-emerald-50 p-3 rounded-xl border border-emerald-200 text-center font-serif font-black text-emerald-900 text-sm sm:text-base overflow-x-auto">
             K · (x, y) = (K·x, K·y)
           </div>
        </div>
      </div>

      <div className="bg-slate-900 text-white rounded-3xl shadow-xl mt-4 border border-slate-800 overflow-hidden flex flex-col">
        <div className="p-5 bg-slate-800/50 border-b border-slate-800">
          <h3 className="font-bold text-lg flex items-center gap-2 text-emerald-400">
            <Rocket size={18} className="animate-pulse"/> Simulator Skalar Zoom
          </h3>
          <p className="text-slate-400 mt-2 text-xs leading-relaxed">
            Geser slider "Skalar K" untuk melihat bagaimana angka biasa bisa meregangkan, memendekkan, atau bahkan membalik arah (jika negatif) sebuah vektor.
          </p>
        </div>
        
        <div className="p-5 flex flex-col gap-6">
          <div className="grid grid-cols-2 gap-4">
            <div className="bg-slate-800 p-3 rounded-xl border border-slate-700">
              <div className="flex justify-between items-center mb-2">
                <label className="text-xs text-indigo-300">Vektor X</label>
                <span className="font-mono text-xs bg-slate-900 px-1.5 py-0.5 rounded text-indigo-300">{vX}</span>
              </div>
              <input type="range" min="-5" max="5" value={vX} onChange={(e) => setVX(parseInt(e.target.value))} className="w-full accent-indigo-500 h-1.5" />
            </div>
            <div className="bg-slate-800 p-3 rounded-xl border border-slate-700">
              <div className="flex justify-between items-center mb-2">
                <label className="text-xs text-indigo-300">Vektor Y</label>
                <span className="font-mono text-xs bg-slate-900 px-1.5 py-0.5 rounded text-indigo-300">{vY}</span>
              </div>
              <input type="range" min="-5" max="5" value={vY} onChange={(e) => setVY(parseInt(e.target.value))} className="w-full accent-indigo-500 h-1.5" />
            </div>
          </div>

          <div className="bg-emerald-900/30 p-4 rounded-xl border border-emerald-800">
            <div className="flex justify-between items-center mb-3">
              <label className="text-sm font-bold text-emerald-400">Pengali Skalar (K)</label>
              <span className="font-black text-lg bg-emerald-800 px-3 py-1 rounded-lg text-white shadow-inner">{scalar}</span>
            </div>
            <input type="range" min="-3" max="3" value={scalar} onChange={(e) => setScalar(parseInt(e.target.value))} className="w-full accent-emerald-400 h-2 rounded-full cursor-pointer" />
          </div>

          <div className="bg-black/40 p-5 rounded-2xl border border-slate-800 text-center shadow-inner">
            <div className="text-xs text-slate-500 mb-2">Perhitungan Skalar × Vektor:</div>
            <div className="flex items-center justify-center gap-2 mb-2">
               <span className="text-emerald-400 font-bold text-lg">{scalar}</span>
               <span className="text-slate-400 text-sm">×</span>
               <span className="text-indigo-300 font-mono bg-indigo-900/30 px-2 py-0.5 rounded text-sm">({vX}, {vY})</span>
            </div>
            <div className="text-slate-600 text-sm mb-2">↓</div>
            <div className="text-2xl sm:text-3xl font-black text-white bg-emerald-600/20 py-3 rounded-xl border border-emerald-500/30">
              ({scalar * vX}, {scalar * vY})
            </div>
            <div className={`mt-4 text-xs font-bold px-3 py-2 rounded-lg inline-block border ${scalar > 0 ? "bg-blue-900/30 text-blue-300 border-blue-800" : scalar < 0 ? "bg-rose-900/30 text-rose-300 border-rose-800" : "bg-slate-800 text-slate-400 border-slate-700"}`}>
              {scalar > 0 ? "Panah SEARAH, mengalami peregangan." : 
               scalar < 0 ? "⚠️ Arah panah BERBALIK 180 Derajat!" : 
               "Vektor hancur menjadi TITIK (Nol)."}
            </div>
          </div>
        </div>
      </div>

      <ExampleBox 
        question={<>Diberikan vektor <Vec>p</Vec> = (2, -1, 3) dan <Vec>q</Vec> = (-3, 4, 1). <br/><br/>Hitunglah hasil operasi Aljabar dari: <br/><b className="text-lg bg-indigo-100 text-indigo-800 px-2 rounded mt-2 inline-block">3<Vec>p</Vec> - 2<Vec>q</Vec></b></>}
        answerSteps={
          <>
            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">Langkah 1: Kalikan Skalar ke Dalam</p>
            <p className="text-xs text-slate-500">Kalikan angka 3 ke dalam <Vec>p</Vec>, dan angka 2 ke dalam <Vec>q</Vec>.</p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap mb-4">
              3<Vec>p</Vec> = 3 × (2, -1, 3) &nbsp;= <b className="text-indigo-600">(6, -3, 9)</b> <br/>
              2<Vec>q</Vec> = 2 × (-3, 4, 1) = <b className="text-emerald-600">(-6, 8, 2)</b>
            </div>

            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">Langkah 2: Kurangkan Hasil Keduanya</p>
            <p className="text-xs text-slate-500">Kurangi masing-masing komponen X dengan X, Y dengan Y, Z dengan Z secara berurutan.</p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap">
              3<Vec>p</Vec> - 2<Vec>q</Vec> = (6, -3, 9) - (-6, 8, 2) <br/>
              3<Vec>p</Vec> - 2<Vec>q</Vec> = ( 6 - (-6), &nbsp;-3 - 8, &nbsp;9 - 2 ) <br/>
              3<Vec>p</Vec> - 2<Vec>q</Vec> = ( 6 + 6, &nbsp;&nbsp;&nbsp;-11, &nbsp;&nbsp;&nbsp;&nbsp;7 ) <br/>
              <span className="mt-2 block bg-emerald-100 text-emerald-800 p-2 rounded text-center border border-emerald-300">
                <b>Hasil = (12, -11, 7)</b>
              </span>
            </div>
          </>
        }
      />
    </div>
  );
};

const PerkalianSkalar = () => {
  const [angle, setAngle] = useState(45);
  
  const rad = (angle * Math.PI) / 180;
  const x = 60 * Math.cos(rad);
  const y = -60 * Math.sin(rad);

  const getDotProductStatus = () => {
    if (angle < 90) return { text: "Positif (>0)", color: "text-emerald-600", desc: "Searah / Saling Bantu", bg: "bg-emerald-100" };
    if (angle == 90) return { text: "Nol (=0)", color: "text-blue-600", desc: "Tegak Lurus (Bebas)", bg: "bg-blue-100" };
    return { text: "Negatif (<0)", color: "text-rose-600", desc: "Berlawanan / Menghambat", bg: "bg-rose-100" };
  };

  const status = getDotProductStatus();

  return (
    <div className="space-y-6 animate-in fade-in duration-500">
      <div className="mb-4">
        <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">5. Dot Product (Kekompakan) 🎯</h2>
        <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">
          Mengalikan dua Vektor dengan "Titik" (Dot Product) itu unik! Kenapa? Karena hasilnya BUKAN vektor baru, melainkan sekadar angka biasa (Skalar).
        </p>
      </div>

      <HeroImage 
        src="https://images.unsplash.com/photo-1581091226825-a6a2a5aee158?auto=format&fit=crop&w=800&q=80" 
        alt="Orang mendorong gerobak"
        caption="Aplikasi Dot Product: Kerja (Fisika). Dorongan maju (v1) VS Arah gerobak (v2). Semakin searah, kerja semakin maksimal!"
      />

      <div className="bg-white border-2 border-purple-100 rounded-3xl p-5 shadow-sm mt-6">
        <div className="flex flex-col gap-5">
           <div className="border-b border-slate-100 pb-5">
              <h3 className="font-bold text-purple-900 text-sm uppercase tracking-wider mb-2 flex gap-2 items-center"><Grid3X3 size={16}/> Jika diketahui Angka Kordinat (x,y,z)</h3>
              <p className="text-xs text-slate-500 mb-2">Kalikan x dgn x, y dgn y, z dgn z, lalu total semuanya.</p>
              <div className="bg-purple-50 text-purple-900 font-serif font-black p-3 rounded-xl border border-purple-200 text-center overflow-x-auto text-sm sm:text-base">
                 <Vec>a</Vec> · <Vec>b</Vec> = (x₁·x₂) + (y₁·y₂) + (z₁·z₂)
              </div>
           </div>
           <div>
              <h3 className="font-bold text-amber-900 text-sm uppercase tracking-wider mb-2 flex gap-2 items-center"><Compass size={16}/> Jika diketahui Sudut dan Panjang</h3>
              <p className="text-xs text-slate-500 mb-2">Gunakan bantuan Trigonometri Cosinus.</p>
              <div className="bg-amber-50 text-amber-900 font-serif font-black p-3 rounded-xl border border-amber-200 text-center overflow-x-auto text-sm sm:text-base">
                 <Vec>a</Vec> · <Vec>b</Vec> = |<Vec>a</Vec>| |<Vec>b</Vec>| cos(&theta;)
              </div>
           </div>
        </div>
      </div>

      <div className="bg-white border-2 border-slate-200 shadow-md rounded-3xl overflow-hidden mt-6 flex flex-col">
        <div className="p-5 bg-slate-50 border-b border-slate-200">
          <h3 className="font-bold text-lg text-slate-800">Cek Kekompakan Sudut</h3>
          <p className="text-xs text-slate-500 mt-1">Geser sudut di bawah untuk melihat bagaimana nilai Dot Product berubah (Positif, Nol, Negatif).</p>
        </div>

        <div className="p-5 flex flex-col items-center gap-6">
          <div className="w-48 h-48 sm:w-56 sm:h-56 bg-slate-50 rounded-full border-4 border-slate-200 flex items-center justify-center relative shadow-inner p-2 shrink-0">
            <svg viewBox="-80 -80 160 160" className="w-full h-full overflow-visible drop-shadow-md">
              <defs>
                <marker id="dot-arr-1" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#3b82f6"/></marker>
                <marker id="dot-arr-2" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#f59e0b"/></marker>
              </defs>
              
              <line x1="0" y1="0" x2="60" y2="0" stroke="#3b82f6" strokeWidth="5" markerEnd="url(#dot-arr-1)"/>
              
              <line x1="0" y1="0" x2={x} y2={y} stroke="#f59e0b" strokeWidth="5" markerEnd="url(#dot-arr-2)">
                <animate attributeName="x2" dur="0.1s" fill="freeze" />
                <animate attributeName="y2" dur="0.1s" fill="freeze" />
              </line>
              
              {angle > 0 && (
                <path d={`M 25 0 A 25 25 0 ${angle > 180 ? 1 : 0} 0 ${25*Math.cos(rad)} ${-25*Math.sin(rad)}`} fill="none" stroke="#94a3b8" strokeWidth="3" strokeDasharray="3,3"/>
              )}
              <circle cx="0" cy="0" r="5" fill="#1e293b"/>
            </svg>
            <div className="absolute top-2 right-2 font-black text-sm bg-white px-2 py-0.5 rounded shadow border border-slate-100">{angle}°</div>
          </div>

          <div className="w-full space-y-4">
            <div className="bg-slate-100 p-3 rounded-xl">
               <div className="flex justify-between text-xs font-bold text-slate-500 uppercase tracking-wide mb-2">
                 <span>Atur Sudut Gesekan</span>
               </div>
               <input 
                  type="range" min="0" max="180" value={angle} 
                  onChange={(e) => setAngle(e.target.value)} 
                  className="w-full accent-slate-700 h-2 bg-slate-300 rounded-lg appearance-none cursor-pointer" 
               />
            </div>
            
            <div className={`p-4 rounded-xl border-2 shadow-sm text-center transition-colors duration-300 ${status.bg} border-current border-opacity-20`}>
              <div className="text-xs font-bold uppercase tracking-wider mb-1 opacity-70">Hasil Dot Product:</div>
              <div className={`text-2xl sm:text-3xl font-black ${status.color}`}>{status.text}</div>
              <div className="text-sm font-bold opacity-80 mt-1 bg-white/50 inline-block px-3 py-1 rounded-full">{status.desc}</div>
            </div>
          </div>
        </div>
      </div>

      <ExampleBox 
        question={<>Diberikan vektor <Vec>a</Vec> = (1, 2, -1) dan <Vec>b</Vec> = (3, 0, 4). <br/><br/>Hitunglah nilai <b>Dot Product</b>-nya, dan tentukan <b>nilai Cosinus sudut</b> yang terbentuk di antara mereka!</>}
        answerSteps={
          <>
            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">1. Hitung Dot Product Dulu</p>
            <p className="text-xs text-slate-500">Kalikan komponen berpasangan lalu jumlahkan.</p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap mb-4">
              <Vec>a</Vec> · <Vec>b</Vec> = (1 × 3) + (2 × 0) + (-1 × 4) <br/>
              <Vec>a</Vec> · <Vec>b</Vec> = 3 + 0 - 4 <br/>
              <Vec>a</Vec> · <Vec>b</Vec> = <b>-1</b>
            </div>

            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">2. Hitung Panjang (Pythagoras) Masing-masing</p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap mb-4">
              |<Vec>a</Vec>| = &radic;(1² + 2² + (-1)²) = &radic;(1 + 4 + 1) = <b>&radic;6</b> <br/>
              |<Vec>b</Vec>| = &radic;(3² + 0² + 4²) = &radic;(9 + 0 + 16) = &radic;25 = <b>5</b>
            </div>

            <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">3. Gabungkan di Rumus Cosinus</p>
            <p className="text-xs text-slate-500">Rumus mencari sudut: Cos(&theta;) = (Dot Product) dibagi (Panjang a × Panjang b).</p>
            <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap">
              cos(&theta;) = (<Vec>a</Vec> · <Vec>b</Vec>) / (|<Vec>a</Vec>| × |<Vec>b</Vec>|) <br/>
              cos(&theta;) = -1 / (&radic;6 × 5) <br/>
              <span className="mt-2 block bg-emerald-100 text-emerald-800 p-2 rounded border border-emerald-300">
                <b>cos(&theta;) = -1 / 5&radic;6</b>
              </span>
            </div>
            <p className="mt-3 text-xs text-rose-700 bg-rose-50 p-3 rounded-lg border border-rose-100 font-medium leading-relaxed">
              💡 <b>Insight:</b> Karena hasil Cosinusnya <b>NEGATIF</b>, maka sudut antara kedua vektor ini dipastikan <b>Tumpul (&gt; 90°)</b> alias berlawanan arah.
            </p>
          </>
        }
      />
    </div>
  );
};

const Perbandingan = () => (
  <div className="space-y-6 animate-in fade-in duration-500">
    <div className="mb-4">
      <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">6. Titik Bagi (Rasio) 📍</h2>
      <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">Seperti Google Maps memecah rute perjalanan Jakarta-Bandung menjadi beberapa pos pemberhentian dengan proporsi jarak tertentu.</p>
    </div>

    <HeroImage 
      src="https://images.unsplash.com/photo-1524661135-423995f22d0b?auto=format&fit=crop&w=800&q=80" 
      alt="Pin lokasi pada peta"
      caption="Mencari letak akurat Rest Area (R) yang membagi jalan tol dari P ke Q dengan rasio 2:1."
    />

    <div className="bg-white border-2 border-slate-200 rounded-3xl p-5 shadow-sm mt-6">
      <h3 className="font-bold text-xl mb-3 text-slate-800">Rumus "Kali Menyilang"</h3>
      <p className="text-slate-600 mb-5 text-sm leading-relaxed">
        Jika titik <b>R</b> membagi ruas <b>P</b> ke <b>Q</b> dengan rasio <MathVar>m : n</MathVar>. Ingat selalu trik ini: <b>Rasio belakang (n) dikali Vektor Depan (p), ditambah Rasio depan (m) dikali Vektor Belakang (q)!</b>
      </p>
      
      <div className="flex flex-col gap-4">
        <div className="bg-indigo-50 border border-indigo-200 p-4 rounded-2xl relative overflow-hidden">
          <div className="font-black text-indigo-900 text-lg mb-1 relative z-10">Titik Bagi Dalam</div>
          <div className="text-xs text-indigo-700 mb-3 relative z-10 font-medium">Titik R berada "di antara" P dan Q.</div>
          <div className="text-center font-serif text-lg text-indigo-900 font-bold bg-white py-3 rounded-xl shadow-sm border border-indigo-100 relative z-10 overflow-x-auto whitespace-nowrap">
            <Vec>r</Vec> = (n·<Vec>p</Vec> + m·<Vec>q</Vec>) / (m + n)
          </div>
        </div>

        <div className="bg-rose-50 border border-rose-200 p-4 rounded-2xl relative overflow-hidden">
          <div className="font-black text-rose-900 text-lg mb-1 relative z-10">Titik Bagi Luar</div>
          <div className="text-xs text-rose-700 mb-3 relative z-10 font-medium">Titik R meleset jauh, melewati Q. (n jadi negatif).</div>
          <div className="text-center font-serif text-lg text-rose-900 font-bold bg-white py-3 rounded-xl shadow-sm border border-rose-100 relative z-10 overflow-x-auto whitespace-nowrap">
            <Vec>r</Vec> = (-n·<Vec>p</Vec> + m·<Vec>q</Vec>) / (m - n)
          </div>
        </div>
      </div>
    </div>

    <Callout title="Bocoran Soal Ujian: Titik Tengah" icon={Target} color="emerald">
      Kalau yang ditanya <b>Titik Tengah</b> persis, berarti rasionya <span className="font-bold bg-emerald-200 px-1 rounded">1 : 1</span>. <br/>
      Rumus menyilangnya otomatis menciut jadi sangat gampang: cukup tambahkan kordinat awal dan akhir, lalu belah dua!<br/>
      <span className="font-mono font-bold block mt-3 text-center text-sm bg-emerald-200/50 py-2 rounded-lg text-emerald-900 border border-emerald-300">Titik Tengah M = (<Vec>p</Vec> + <Vec>q</Vec>) / 2</span>
    </Callout>

    <ExampleBox 
      question={<>Diketahui titik P(2, -1, 4) dan titik Q(7, 4, -1). <br/><br/>Sebuah titik R membagi ruas garis PQ di dalam dengan <b>perbandingan 2 : 3</b>. Cari letak koordinat R!</>}
      answerSteps={
        <>
          <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">1. Identifikasi Rasio & Kali Menyilang</p>
          <ul className="list-disc pl-5 mb-3 text-sm text-slate-600">
             <li>Rasio Depan <MathVar>m = 2</MathVar></li>
             <li>Rasio Belakang <MathVar>n = 3</MathVar></li>
             <li>Terapkan menyilang: <b>3</b> dikali P, dan <b>2</b> dikali Q.</li>
          </ul>
          
          <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap mb-4">
            <span className="text-slate-400">// Hitung perkalian silangnya dulu:</span><br/>
            n·<Vec>p</Vec> = 3 × (2, -1, 4) = (6, -3, 12)<br/>
            m·<Vec>q</Vec> = 2 × (7, 4, -1) = (14, 8, -2)<br/>
            <br/>
            <span className="text-slate-400">// Tambahkan:</span><br/>
            (n·<Vec>p</Vec> + m·<Vec>q</Vec>) = (6+14, -3+8, 12-2) <br/>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = <b>(20, 5, 10)</b>
          </div>

          <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">2. Dibagi Total Rasio</p>
          <p className="text-xs text-slate-500">Bagian bawah rumus adalah total rasio (m+n) yaitu 2 + 3 = 5.</p>
          <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap">
            <Vec>r</Vec> = (20, 5, 10) / 5 <br/>
            <span className="mt-2 block bg-emerald-100 text-emerald-800 p-2 rounded border border-emerald-300">
                <Vec>r</Vec> = <b>(4, 1, 2)</b>
            </span>
          </div>
          <p className="mt-2 text-xs font-bold text-indigo-700 bg-indigo-50 p-2 rounded-lg text-center">Posisi koordinat pembagi R adalah di (4, 1, 2).</p>
        </>
      }
    />
  </div>
);

const Proyeksi = () => (
  <div className="space-y-6 animate-in fade-in duration-500">
    <div className="mb-4">
      <h2 className="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-tight leading-tight">7. Proyeksi Ortogonal 🔦</h2>
      <p className="text-slate-500 mt-2 text-sm sm:text-base leading-relaxed">Menjatuhkan "Bayangan" tegak lurus. Berapa banyak vektor dorongmu yang benar-benar tersalurkan maju ke depan?</p>
    </div>

    <HeroImage 
      src="https://images.unsplash.com/photo-1534351590666-13e3e96b5017?auto=format&fit=crop&w=800&q=80" 
      alt="Bayangan orang di jalan"
      caption="Sorot senter tepat lurus dari atas. Bayangan hitam yang nempel di aspal itu yang disebut Proyeksi."
    />

    <div className="bg-white border-2 border-slate-200 rounded-3xl overflow-hidden shadow-sm flex flex-col">
      <div className="w-full bg-slate-900 p-6 flex justify-center relative overflow-hidden group min-h-[220px] items-center">
         {/* Flashlight Beam */}
         <div className="absolute top-0 left-1/2 w-32 h-64 bg-yellow-200/20 blur-2xl transform -translate-x-1/2 rounded-full"></div>
         <svg viewBox="0 0 400 160" className="w-full max-w-[350px] drop-shadow-2xl z-10" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <marker id="p1" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#818cf8"/></marker>
            <marker id="p2" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#34d399"/></marker>
            <marker id="p3" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L0,5 L5,2.5 z" fill="#fbbf24"/></marker>
          </defs>

          {/* Senter jatuh */}
          <line x1="160" y1="20" x2="160" y2="120" stroke="#fef08a" strokeWidth="1" strokeDasharray="5,3" opacity="0.6"/>
          
          <line x1="30" y1="120" x2="350" y2="120" stroke="#34d399" strokeWidth="4" markerEnd="url(#p2)"/>
          <line x1="30" y1="120" x2="160" y2="30" stroke="#818cf8" strokeWidth="5" markerEnd="url(#p1)"/>
          
          {/* Garis batas proyeksi (animasi) */}
          <line x1="160" y1="30" x2="160" y2="120" stroke="#fcd34d" strokeWidth="2.5" strokeDasharray="6,4">
             <animate attributeName="stroke-dashoffset" values="40;0" dur="1s" repeatCount="indefinite"/>
          </line>
          
          {/* Shadow vector */}
          <line x1="30" y1="120" x2="158" y2="120" stroke="#fbbf24" strokeWidth="6" markerEnd="url(#p3)"/>
          
          {/* Siku-siku */}
          <rect x="145" y="105" width="15" height="15" fill="none" stroke="#fcd34d" strokeWidth="2"/>
          
          <text x="320" y="145" fontSize="14" fill="#34d399" fontWeight="bold">Lantai (v)</text>
          <text x="60" y="55" fontSize="14" fill="#818cf8" fontWeight="bold">Tongkat (u)</text>
          <text x="40" y="145" fontSize="14" fill="#fbbf24" fontWeight="bold">Bayangan</text>
          <circle cx="30" cy="120" r="5" fill="#f8fafc"/>
        </svg>
      </div>

      <div className="p-5">
        <h3 className="font-bold text-lg mb-3 text-slate-800">Dua Jenis Jawaban Proyeksi</h3>
        <p className="text-slate-600 text-sm leading-relaxed mb-4">
          Saat disuruh mencari "Proyeksi u pada v" (artinya v bertindak jadi lantainya), pastikan di soal yang dicari itu sekadar Angka panjangnya, atau Vektor panah barunya?
        </p>
        <div className="flex flex-col gap-3">
           <div className="bg-amber-50 border-l-4 border-amber-500 p-4 rounded-xl shadow-sm">
              <span className="font-black text-amber-900 block text-sm mb-1 uppercase tracking-wider">1. Proyeksi Skalar (Angka)</span>
              <span className="text-xs text-amber-700 mb-2 block">Menghasilkan nilai seberapa panjang bayangannya.</span>
              <div className="font-serif text-sm sm:text-base text-amber-900 font-bold bg-white px-3 py-2 rounded-lg border border-amber-200 text-center overflow-x-auto">
                |c| = (<Vec>u</Vec> · <Vec>v</Vec>) / |<Vec>v</Vec>|
              </div>
           </div>
           <div className="bg-indigo-50 border-l-4 border-indigo-500 p-4 rounded-xl shadow-sm">
              <span className="font-black text-indigo-900 block text-sm mb-1 uppercase tracking-wider">2. Proyeksi Vektor (Arah)</span>
              <span className="text-xs text-indigo-700 mb-2 block">Menghasilkan koordinat (x,y,z) dari panah bayangan tersebut.</span>
              <div className="font-serif text-sm sm:text-base text-indigo-900 font-bold bg-white px-3 py-2 rounded-lg border border-indigo-200 text-center overflow-x-auto">
                <Vec>c</Vec> = [(<Vec>u</Vec> · <Vec>v</Vec>) / |<Vec>v</Vec>|²] <Vec>v</Vec>
              </div>
           </div>
        </div>
      </div>
    </div>

    <ExampleBox 
      question={<>Diberikan vektor <Vec>u</Vec> = (2, -1, 3) dan vektor alas <Vec>v</Vec> = (1, 2, 2). <br/><br/>Tentukan nilai <b>Proyeksi Skalar Ortogonal</b> dari vektor <Vec>u</Vec> pada <Vec>v</Vec> !</>}
      answerSteps={
        <>
          <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2">Tahap 1: Pahami Maunya Soal</p>
          <p className="text-xs text-slate-600 mb-2">Ditanya "Skalar" berarti cukup pakai rumus pendek (hanya cari angkanya). Posisi "pada v" berarti v jadi pembagi di bawah akar.</p>
          
          <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2 mt-4">Tahap 2: Siapkan Bahan-bahannya</p>
          <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-xs sm:text-sm overflow-x-auto whitespace-nowrap mb-4">
            <span className="text-slate-400">// Cari Dot Product atas</span><br/>
            <Vec>u</Vec> · <Vec>v</Vec> = (2 × 1) + (-1 × 2) + (3 × 2) <br/>
            <Vec>u</Vec> · <Vec>v</Vec> = 2 - 2 + 6 = <b>6</b> <br/><br/>
            
            <span className="text-slate-400">// Cari Panjang alas v (di bawah)</span><br/>
            |<Vec>v</Vec>| = &radic;(1² + 2² + 2²) <br/>
            |<Vec>v</Vec>| = &radic;(1 + 4 + 4) = &radic;9 = <b>3</b>
          </div>

          <p className="font-bold text-indigo-800 border-l-2 border-indigo-400 pl-2 mt-4">Tahap 3: Eksekusi Dibagi</p>
          <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-sm sm:text-base text-center">
            P. Skalar = 6 / 3 = <b className="text-xl text-rose-600">2</b>
          </div>
          <p className="mt-2 text-xs font-bold text-slate-500 text-center">
            Panjang bayangan murni yang jatuh ke alas V adalah 2 satuan panjang.
          </p>
        </>
      }
    />
  </div>
);

const Kegunaan = () => {
  const applications = [
    {
      icon: <Wind className="text-sky-600" size={26} />,
      bg: "bg-sky-100 border-sky-200",
      image: "https://images.unsplash.com/photo-1436491865332-7a61a109cc05?auto=format&fit=crop&w=600&q=80",
      title: "Penerbangan & Crosswind",
      desc: "Pesawat di udara tidak seperti mobil di jalan aspal. Saat terbang lurus ke depan dengan kecepatan 500 km/jam, pesawat juga didorong angin kencang dari arah samping (crosswind). Pilot dan sistem autopilot harus menggunakan vektor penjumlahan untuk menyesuaikan 'moncong' pesawat (heading) agar arah terbang sebenarnya (track) tepat menuju bandara tujuan.",
      calcTitle: "Contoh Kasus Navigasi",
      calcQ: "Pesawat melaju ke Utara kecepatan 400 km/jam. Tiba-tiba ada angin bertiup kencang ke arah Timur dengan kecepatan 300 km/jam. Berapa kecepatan gerak pesawat sebenarnya (Resultan)?",
      calcA: <>
        <p>Karena Utara dan Timur membentuk sudut 90 derajat, kita cukup gunakan teorema Pythagoras!</p>
        <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-sm my-2 text-center overflow-x-auto">
           V<sub>resultan</sub> = &radic;(400² + 300²) <br/>
           = &radic;(160000 + 90000) <br/>
           = &radic;250000 = <b className="text-rose-600">500 km/jam</b>
        </div>
        <p className="text-xs text-slate-600">Pesawat tersebut sebenarnya bergerak menyamping ke arah Timur Laut dengan kecepatan 500 km/jam relatif terhadap tanah (bukan 400 km/jam lagi).</p>
      </>
    },
    {
      icon: <Building2 className="text-amber-600" size={26} />,
      bg: "bg-amber-100 border-amber-200",
      image: "https://images.unsplash.com/photo-1541888086425-d81bb19240f5?auto=format&fit=crop&w=600&q=80",
      title: "Teknik Sipil: Keseimbangan Statis",
      desc: "Gedung pencakar langit dan jembatan gantung (seperti Jembatan Suramadu) dirancang agar diam tak bergerak meskipun ditarik gravitasi dan ditahan oleh ribuan kabel baja. Insinyur sipil memecah setiap tarikan kabel menjadi vektor. Syarat utama jembatan tidak runtuh adalah: Total Penjumlahan semua vektor gaya dari segala arah mutlak = 0 (Vektor Nol).",
      calcTitle: "Contoh Kasus Statika",
      calcQ: "Sebuah lampu gantung ditarik oleh kabel A dengan gaya (3, 4) Newton dan kabel B dengan gaya (-3, 6) Newton. Berapa gaya total ke bawah yang harus ditahan oleh plafon (Resultan Gaya)?",
      calcA: <>
        <p>Kita hanya perlu menjumlahkan kedua vektor gaya tersebut secara aljabar (komponen demi komponen).</p>
        <div className="bg-slate-100 p-3 rounded-xl border border-slate-200 font-mono text-sm my-2 text-center">
           <Vec>F</Vec><sub>total</sub> = (3, 4) + (-3, 6)<br/>
           <Vec>F</Vec><sub>total</sub> = (3 - 3, 4 + 6)<br/>
           <Vec>F</Vec><sub>total</sub> = <b className="text-emerald-600">(0, 10)</b>
        </div>
        <p className="text-xs text-slate-600">Terlihat di sumbu X nilainya 0 (tidak goyang ke kiri/kanan), dan tertarik ke atas dengan gaya total 10 N.</p>
      </>
    },
    {
      icon: <Cpu className="text-emerald-600" size={26} />,
      bg: "bg-emerald-100 border-emerald-200",
      image: "https://images.unsplash.com/photo-1620712943543-bcc4688e7485?auto=format&fit=crop&w=600&q=80",
      title: "Kecerdasan Buatan (AI) & Rekomendasi",
      desc: "Kenapa Spotify tahu lagu yang kamu suka? Kenapa ChatGPT mengerti maksud kalimatmu? Di dalam AI, setiap lagu atau kata diubah menjadi 'angka vektor' (disebut Word Embedding). Untuk mencari dua lagu yang mirip, AI menghitung sudut antara vektor lagu tersebut menggunakan rumus Cosine Similarity (turunan langsung dari rumus Dot Product vektor 3D yang kita pelajari!)."
    },
    {
      icon: <Camera className="text-purple-600" size={26} />,
      bg: "bg-purple-100 border-purple-200",
      image: "https://images.unsplash.com/photo-1552820728-8b83bb6b773f?auto=format&fit=crop&w=600&q=80",
      title: "Grafika Komputer & Game Engine 3D",
      desc: "Dalam game seperti Genshin Impact atau rendering film animasi, cahaya matahari (Lighting) diproses dengan sangat nyata. Komputer secara intensif menghitung Dot Product antara vektor 'arah datangnya cahaya' dan vektor 'arah hadap permukaan objek' untuk menentukan sisi mana yang terang dan sisi mana yang gelap/membentuk bayangan (Proyeksi Ortogonal)."
    }
  ];

  return (
    <div className="space-y-6 animate-in fade-in duration-500">
      <div className="mb-8 text-center pt-2">
        <h2 className="text-2xl sm:text-4xl font-extrabold text-slate-800 tracking-tight leading-tight mb-3">Vektor di Dunia Nyata 🌍</h2>
        <p className="text-slate-600 text-sm sm:text-base max-w-2xl mx-auto leading-relaxed px-2">Vektor bukan sekadar kumpulan panah dan angka abstrak di atas kertas ujian. Mereka adalah "bahasa mesin" pembangun teknologi masa kini.</p>
      </div>

      <div className="flex flex-col gap-8">
        {applications.map((app, idx) => (
          <div key={idx} className={`bg-white rounded-3xl overflow-hidden shadow-sm border-2 ${app.bg} flex flex-col group relative`}>
            
            {/* Decorative Background Element */}
            <div className="absolute top-0 right-0 w-32 h-32 bg-white/40 rounded-full blur-2xl transform translate-x-1/3 -translate-y-1/4 pointer-events-none"></div>

            <div className="h-44 sm:h-52 overflow-hidden relative">
              <img src={app.image} alt={app.title} className="w-full h-full object-cover transform group-hover:scale-[1.03] transition-transform duration-700" loading="lazy" />
              <div className="absolute inset-0 bg-gradient-to-t from-slate-900/95 via-slate-900/40 to-transparent flex items-end p-5">
                 <h3 className="font-bold text-xl sm:text-2xl text-white tracking-wide">{app.title}</h3>
              </div>
              <div className={`absolute top-4 right-4 bg-white p-2.5 rounded-2xl shadow-xl transform group-hover:-rotate-6 transition-transform duration-300`}>
                {app.icon}
              </div>
            </div>
            
            <div className="p-5 sm:p-6 bg-white flex flex-col gap-4">
              <p className="text-slate-600 text-sm sm:text-base leading-relaxed">{app.desc}</p>
              
              {/* Optional Math Application Example */}
              {app.calcQ && (
                <div className="mt-2 border-t border-slate-100 pt-4">
                   <ExampleBox 
                      customTitle={app.calcTitle}
                      question={app.calcQ}
                      answerSteps={app.calcA}
                   />
                </div>
              )}
            </div>
          </div>
        ))}
      </div>
      
      <div className="mt-12 bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] bg-slate-900 rounded-3xl p-8 text-center text-white shadow-xl relative overflow-hidden">
        <div className="absolute top-0 right-0 w-40 h-40 bg-indigo-500/30 rounded-full blur-3xl transform translate-x-1/2 -translate-y-1/2 pointer-events-none"></div>
        <div className="absolute bottom-0 left-0 w-40 h-40 bg-rose-500/30 rounded-full blur-3xl transform -translate-x-1/2 translate-y-1/2 pointer-events-none"></div>
        
        <div className="relative z-10 flex flex-col items-center">
           <div className="bg-indigo-500/30 p-4 rounded-full mb-4">
              <CheckCircle2 size={36} className="text-indigo-200"/>
           </div>
           <h3 className="text-2xl sm:text-3xl font-black mb-3">Selamat, Modul Selesai! 🎉</h3>
           <p className="text-slate-300 text-sm sm:text-base max-w-md leading-relaxed mb-6">Kamu telah sukses menaklukkan bab paling esensial dalam Fisika dan Matematika tingkat lanjut. Pertahankan semangat analisismu!</p>
           <button onClick={() => window.scrollTo({ top: 0, behavior: 'smooth' })} className="px-6 py-3 bg-white text-slate-900 rounded-xl font-bold text-sm shadow-lg hover:scale-105 transition-transform active:scale-95">
              Kembali ke Awal
           </button>
        </div>
      </div>
    </div>
  );
};

// --- App Layout & Navigation State ---

const sections = [
  { id: 'definisi', title: '1. Mengenal Vektor', icon: BookOpen, component: Definisi },
  { id: 'geometris', title: '2. Gambar & Panah', icon: Compass, component: Geometris },
  { id: 'analitik', title: '3. Sistem Koordinat', icon: Grid3X3, component: Analitik },
  { id: 'operasi', title: '4. Aljabar Hitung', icon: PlusSquare, component: Operasi },
  { id: 'dotproduct', title: '5. Skalar & Dot', icon: Orbit, component: PerkalianSkalar },
  { id: 'perbandingan', title: '6. Rumus Rasio', icon: MapPin, component: Perbandingan },
  { id: 'proyeksi', title: '7. Proyeksi Bayangan', icon: ArrowDownToLine, component: Proyeksi },
  { id: 'kegunaan', title: '8. Aplikasi Nyata', icon: Globe, component: Kegunaan },
];

export default function App() {
  const [activeSection, setActiveSection] = useState(0);
  const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false);

  // Mencegah body scrolling saat menu mobile terbuka
  useEffect(() => {
    if (isMobileMenuOpen) {
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = 'unset';
    }
    return () => { document.body.style.overflow = 'unset'; }
  }, [isMobileMenuOpen]);

  const ActiveComponent = sections[activeSection].component;

  const navigateTo = (index) => {
    setActiveSection(index);
    setIsMobileMenuOpen(false);
    document.getElementById('main-scroll-area')?.scrollTo({ top: 0, behavior: 'smooth' });
  };

  return (
    <div className="flex h-screen bg-slate-50 font-sans text-slate-900 overflow-hidden selection:bg-indigo-200">
      
      {/* Mobile Top Navbar (Fixed) */}
      <div className="md:hidden fixed top-0 left-0 right-0 h-[60px] bg-white border-b border-slate-200 z-40 flex items-center justify-between px-4 shadow-sm">
        <div className="font-extrabold text-lg text-indigo-900 flex items-center gap-2">
          <div className="bg-gradient-to-br from-indigo-500 to-purple-600 text-white p-1.5 rounded-lg">
            <Orbit size={18} />
          </div>
          Vektor Seru!
        </div>
        <button 
          onClick={() => setIsMobileMenuOpen(!isMobileMenuOpen)} 
          className="p-2 text-slate-600 bg-slate-100 rounded-lg active:bg-slate-200 transition-colors"
          aria-label="Toggle Menu"
        >
          {isMobileMenuOpen ? <X size={20} /> : <Menu size={20} />}
        </button>
      </div>

      {/* Mobile Overlay Background */}
      {isMobileMenuOpen && (
        <div 
          className="md:hidden fixed inset-0 bg-slate-900/40 z-30 backdrop-blur-sm transition-opacity" 
          onClick={() => setIsMobileMenuOpen(false)} 
        />
      )}

      {/* Sidebar Navigation */}
      <div className={`
        fixed md:static inset-y-0 left-0 z-40
        w-[280px] bg-white border-r border-slate-200 shadow-2xl md:shadow-none
        transform transition-transform duration-300 ease-in-out flex flex-col
        ${isMobileMenuOpen ? "translate-x-0" : "-translate-x-full md:translate-x-0"}
      `}>
        <div className="h-[60px] md:h-[80px] flex items-center px-6 border-b border-slate-100 shrink-0">
          <div className="font-black text-xl md:text-2xl text-slate-800 flex items-center gap-3">
            <div className="bg-gradient-to-br from-indigo-500 to-purple-600 text-white p-2 rounded-xl shadow-md transform rotate-3">
              <Orbit size={24} />
            </div>
            <span className="hidden md:inline">Vektor Seru! 🚀</span>
            <span className="md:hidden text-lg">Daftar Materi</span>
          </div>
        </div>
        
        <div className="flex-1 overflow-y-auto py-5 px-3 md:px-4 space-y-1 custom-scrollbar pb-24 md:pb-6">
          <div className="text-[10px] md:text-xs font-black text-slate-400 uppercase tracking-widest mb-3 px-3">Modul Belajar</div>
          
          {sections.map((sec, idx) => {
            const Icon = sec.icon;
            const isActive = activeSection === idx;
            return (
              <button
                key={sec.id}
                onClick={() => navigateTo(idx)}
                className={`
                  w-full flex items-center gap-3 px-3 py-3 md:py-3.5 rounded-2xl text-left transition-all duration-200 group relative overflow-hidden active:scale-95
                  ${isActive 
                    ? "bg-indigo-600 text-white font-bold shadow-md transform md:scale-[1.02]" 
                    : "text-slate-600 hover:bg-slate-50 hover:text-indigo-600 font-medium"}
                `}
              >
                {/* Active Indicator Glow */}
                {isActive && <div className="absolute left-0 top-0 bottom-0 w-1.5 bg-white/30 rounded-r-full"></div>}
                
                <div className={`
                  w-8 h-8 rounded-xl flex items-center justify-center transition-colors relative z-10 shrink-0
                  ${isActive ? "bg-white/20 text-white shadow-inner" : "bg-slate-100 text-slate-500 group-hover:bg-indigo-100 group-hover:text-indigo-600"}
                `}>
                  <Icon size={16} />
                </div>
                <span className="flex-1 relative z-10 text-sm">{sec.title}</span>
                {isActive && <ChevronRight size={16} className="text-white/70 relative z-10 shrink-0" />}
              </button>
            );
          })}
        </div>
      </div>

      {/* Main Content Area */}
      <div className="flex-1 flex flex-col h-screen overflow-hidden pt-[60px] md:pt-0 relative bg-slate-50/95">
        <main id="main-scroll-area" className="flex-1 overflow-y-auto p-4 sm:p-6 md:p-8 lg:px-12 xl:px-24 scroll-smooth">
          <div className="max-w-3xl mx-auto pb-28 pt-2">
            
            {/* Top Progress Bar */}
            <div className="w-full bg-slate-200/80 h-1.5 sm:h-2 rounded-full mb-6 sm:mb-8 overflow-hidden shadow-inner">
               <div 
                  className="bg-gradient-to-r from-indigo-500 via-purple-500 to-rose-500 h-full rounded-full transition-all duration-700 ease-out relative"
                  style={{ width: `${((activeSection + 1) / sections.length) * 100}%` }}
               >
               </div>
            </div>

            {/* Load the actual section */}
            <ActiveComponent />
            
            {/* Footer Navigation Buttons */}
            <div className="flex justify-between items-center mt-12 sm:mt-16 pt-6 sm:pt-8 border-t-2 border-slate-200/80 gap-3">
              <button 
                disabled={activeSection === 0}
                onClick={() => navigateTo(Math.max(0, activeSection - 1))}
                className={`flex-1 sm:flex-none justify-center px-4 sm:px-6 py-3.5 rounded-2xl text-sm font-bold transition-all flex items-center gap-2 ${activeSection === 0 ? "text-slate-400 bg-slate-100 cursor-not-allowed opacity-50" : "text-indigo-700 bg-indigo-100 hover:bg-indigo-200 active:scale-95 shadow-sm"}`}
              >
                &larr; <span className="hidden sm:inline">Balik</span>
              </button>
              
              <div className="text-xs font-bold text-slate-400">
                {activeSection + 1} / {sections.length}
              </div>

              <button 
                disabled={activeSection === sections.length - 1}
                onClick={() => navigateTo(Math.min(sections.length - 1, activeSection + 1))}
                className={`flex-1 sm:flex-none justify-center px-4 sm:px-6 py-3.5 rounded-2xl text-sm font-bold transition-all flex items-center gap-2 ${activeSection === sections.length - 1 ? "text-slate-400 bg-slate-100 cursor-not-allowed opacity-50" : "text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:shadow-lg hover:scale-105 active:scale-95 shadow-md"}`}
              >
                <span className="hidden sm:inline">Lanjut</span> Gas! &rarr;
              </button>
            </div>
          </div>
        </main>
      </div>

    </div>
  );
}