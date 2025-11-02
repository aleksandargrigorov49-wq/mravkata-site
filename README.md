# mravkata-site
// "Мравката" — Responsive React website with Gallery Carousel + Deploy Instructions // How to use: // 1) Create a React project (Vite recommended): //    npm create vite@latest mravkata --template react // 2) Install dependencies: //    npm install tailwindcss framer-motion lucide-react react-slick slick-carousel // 3) Configure Tailwind (follow tailwindcss.com docs) // 4) Replace src/App.jsx with this file // 5) Run locally: npm run dev // 6) Deploy: //    - GitHub + Vercel: push repo and import on vercel.com //    - or Netlify: drag-and-drop the dist/ folder after npm run build //    - GitHub Actions example: //        on: [push] //        jobs: //          build-deploy: //            runs-on: ubuntu-latest //            steps: //              - uses: actions/checkout@v3 //              - run: npm ci && npm run build //              - uses: JamesIves/github-pages-deploy-action@v4 //                with: //                  folder: dist

import React, { useState } from 'react'; import { motion } from 'framer-motion'; import { Menu, X, Phone, Mail, Image, CalendarCheck } from 'lucide-react'; import Slider from 'react-slick'; import 'slick-carousel/slick/slick.css'; import 'slick-carousel/slick/slick-theme.css';

export default function App(){ const [openNav, setOpenNav] = useState(false); const [showThanks, setShowThanks] = useState(false); const [form, setForm] = useState({parent:'', child:'', age:'', phone:'', email:'', note:''}); const handleChange = e => setForm({...form, [e.target.name]: e.target.value}); const handleSubmit = e => { e.preventDefault(); console.log('Записване:', form); setShowThanks(true); setForm({parent:'', child:'', age:'', phone:'', email:'', note:''}); setTimeout(()=>setShowThanks(false),4000); }

return ( <div className="min-h-screen bg-white text-gray-900 font-sans"> {/* Header */} <header className="sticky top-0 bg-white/90 backdrop-blur-sm border-b z-30"> <div className="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between"> <div className="flex items-center gap-3"> <div className="w-10 h-10 rounded-full bg-pink-100 flex items-center justify-center shadow-sm"> <span className="text-pink-600 font-bold">Мр</span> </div> <div> <div className="text-sm md:text-base font-semibold">Мравката</div> <div className="text-xs text-gray-500">Детска частна занималня</div> </div> </div>

<nav className="hidden md:flex gap-6 text-sm">
        <a href="#home" className="hover:text-pink-600">Начало</a>
        <a href="#about" className="hover:text-pink-600">За нас</a>
        <a href="#program" className="hover:text-pink-600">Програма</a>
        <a href="#gallery" className="hover:text-pink-600">Галерия</a>
        <a href="#contact" className="hover:text-pink-600">Контакти</a>
      </nav>

      <button className="md:hidden p-2 rounded-md" onClick={()=>setOpenNav(!openNav)} aria-label="menu">
        {openNav ? <X size={20}/> : <Menu size={20}/>}
      </button>
    </div>
    {openNav && (
      <nav className="md:hidden max-w-6xl mx-auto px-4 pb-4">
        <div className="flex flex-col gap-3 text-sm">
          <a href="#home">Начало</a>
          <a href="#about">За нас</a>
          <a href="#program">Програма</a>
          <a href="#gallery">Галерия</a>
          <a href="#contact">Контакти</a>
        </div>
      </nav>
    )}
  </header>

  <main className="max-w-6xl mx-auto px-4">
    {/* Hero */}
    <section id="home" className="py-10 flex flex-col md:flex-row items-center gap-10">
      <motion.div initial={{opacity:0, y:10}} animate={{opacity:1,y:0}} transition={{duration:0.6}} className="md:w-1/2">
        <h1 className="text-3xl md:text-5xl font-extrabold leading-tight">Добре дошли в <span className="text-pink-600">Мравката</span></h1>
        <p className="mt-3 text-lg text-gray-600">Топла и сигурна занималня, където всяко дете расте чрез игра и творчество.</p>
        <div className="mt-5 flex gap-3">
          <a href="#program" className="px-5 py-3 bg-pink-600 text-white rounded-lg font-medium shadow">Виж програмата</a>
          <a href="#contact" className="px-5 py-3 border rounded-lg">Запази място</a>
        </div>
      </motion.div>
      <div className="md:w-1/2 flex justify-center">
        <div className="w-64 h-64 bg-pink-50 rounded-full flex items-center justify-center">
          <p className="text-gray-400">[Снимка / илюстрация]</p>
        </div>
      </div>
    </section>

    {/* About */}
    <section id="about" className="py-12">
      <div className="grid md:grid-cols-2 gap-8 items-center">
        <div>
          <h2 className="text-2xl font-semibold">За нас</h2>
          <p className="mt-3 text-gray-700 text-sm md:text-base">„Мравката" е уютна занималня, фокусирана върху детското развитие чрез игра, музика и творчество. Нашият екип работи с индивидуален подход към всяко дете.</p>
          <div className="mt-4 grid grid-cols-1 sm:grid-cols-2 gap-3">
            <InfoCard icon={<CalendarCheck size={18}/>} title="Гъвкаво време" text="Работим всеки ден от 8:00 до 18:00" />
            <InfoCard icon={<Phone size={18}/>} title="Безопасност" text="Малък брой деца и квалифицирани педагози" />
          </div>
        </div>
        <div className="h-64 bg-yellow-50 rounded-xl flex items-center justify-center">[Снимка на екипа]</div>
      </div>
    </section>

    {/* Program */}
    <section id="program" className="py-12">
      <h2 className="text-2xl font-semibold text-center">Програма и дейности</h2>
      <div className="mt-8 grid md:grid-cols-3 gap-6">
        <ProgramCard title="Игрова терапия" desc="Сензорни игри и социални упражнения."/>
        <ProgramCard title="Творчески работилници" desc="Рисуване, моделиране, апликации."/>
        <ProgramCard title="Музика и ритъм" desc="Песнички и упражнения за реч и координация."/>
      </div>
    </section>

    {/* Gallery */}
    <section id="gallery" className="py-12">
      <h2 className="text-2xl font-semibold text-center">Галерия</h2>
      <p className="text-center text-gray-600 mt-2">Нашите усмивки и занимания</p>
      <div className="mt-6">
        <GalleryCarousel />
      </div>
    </section>

    {/* Contact */}
    <section id="contact" className="py-12">
      <h2 className="text-2xl font-semibold text-center">Контакти и записване</h2>
      <p className="text-center text-gray-600 mt-2">Попълнете формата и ще се свържем с вас за потвърждение.</p>

      <div className="mt-6 max-w-lg mx-auto">
        <form onSubmit={handleSubmit} className="bg-pink-50 p-5 rounded-xl border space-y-3">
          <Input label="Име на родителя" name="parent" value={form.parent} onChange={handleChange} required />
          <Input label="Име на детето" name="child" value={form.child} onChange={handleChange} required />
          <Input label="Възраст" name="age" value={form.age} onChange={handleChange} type="number" min="1" max="12" required />
          <Input label="Телефон" name="phone" value={form.phone} onChange={handleChange} required />
          <Input label="Email (по избор)" name="email" value={form.email} onChange={handleChange} type="email" />
          <div>
            <label className="block text-sm text-gray-700 mb-1">Бележка</label>
            <textarea name="note" value={form.note} onChange={handleChange} className="w-full px-3 py-2 rounded border" rows={3}></textarea>
          </div>
          <button type="submit" className="w-full py-3 rounded-lg bg-yellow-300 text-gray-900 font-semibold">Изпрати заявка</button>
        </form>
        {showThanks && (<div className="mt-4 p-3 bg-green-50 border text-green-800 rounded">Благодарим! Ще се свържем скоро.</div>)}
      </div>

      <div className="mt-8 grid md:grid-cols-3 text-center text-sm text-gray-600 gap-3">
        <div><Phone className="inline mr-1" size={14}/>телефон: (ще добавиш)</div>
        <div><Mail className="inline mr-1" size={14}/>имейл: (ще добавиш)</div>
        <div><Image className="inline mr-1" size={14}/>адрес: (ще добавиш)</div>
      </div>
    </section>
  </main>

  <footer className="bg-white border-t mt-8">
    <div className="max-w-6xl mx-auto px-4 py-6 text-center text-xs text-gray-500">© {new Date().getFullYear()} Мравката — Всички права запазени</div>
  </footer>
</div>

); }

// Components function InfoCard({icon, title, text}){ return ( <div className="p-4 bg-white rounded-lg border flex items-start gap-3 shadow-sm"> <div className="p-2 rounded bg-pink-50">{icon}</div> <div> <div className="font-medium text-sm">{title}</div> <div className="text-xs text-gray-600">{text}</div> </div> </div> ); }

function ProgramCard({title, desc}){ return ( <div className="p-5 bg-white rounded-lg border shadow-sm hover:shadow-md transition"> <div className="font-semibold">{title}</div> <div className="text-sm text-gray-600 mt-1">{desc}</div> </div> ); }

function GalleryCarousel(){ const settings = { dots: true, infinite: true, speed: 500, slidesToShow: 1, slidesToScroll: 1, autoplay: true, autoplaySpeed: 3000, }; const images = [ '/images/gallery1.jpg', '/images/gallery2.jpg', '/images/gallery3.jpg' ]; return ( <Slider {...settings}> {images.map((src,i)=>( <div key={i} className="px-2"> <div className="h-64 md:h-96 bg-gray-100 rounded-xl overflow-hidden flex items-center justify-center"> <img src={src} alt={Галерия ${i+1}} className="w-full h-full object-cover" /> </div> </div> ))} </Slider> ); }

function Input({label, name, value, onChange, type='text', required=false, min, max}){ return ( <div> <label className="block text-sm text-gray-700 mb-1">{label}</label> <input name={name} value={value} onChange={onChange} type={type} required={required} min={min} max={max} className="w-full px-3 py-2 rounded border" /> </div> ); }
