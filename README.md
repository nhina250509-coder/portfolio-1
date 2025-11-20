import React, { useState, useEffect } from 'react';

// アイコンコンポーネント (Lucide iconsの代用としてインラインSVGを使用し、依存関係を排除して確実に表示させる)
const IconMenu = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><line x1="3" y1="12" x2="21" y2="12"></line><line x1="3" y1="6" x2="21" y2="6"></line><line x1="3" y1="18" x2="21" y2="18"></line></svg>
);
const IconX = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
);
const IconArrowRight = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><line x1="5" y1="12" x2="19" y2="12"></line><polyline points="12 5 19 12 12 19"></polyline></svg>
);
const IconGithub = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
);
const IconTwitter = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M22 4s-.7 2.1-2 3.4c1.6 10-9.4 17.3-12.7 14.6-5.5-4.5-1.5-7.2-1.5-7.2-1 1.1-3.5 1.3-4.4-1.5 0 0-1.6-6.1 2.6-7.4 4.2-1.3 15-3.9 15-3.9z"></path></svg>
);
const IconMail = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></svg>
);
const IconExternalLink = ({ className }) => (
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path><polyline points="15 3 21 3 21 9"></polyline><line x1="10" y1="14" x2="21" y2="3"></line></svg>
);

// メインアプリケーションコンポーネント
export default function App() {
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [activeSection, setActiveSection] = useState('home');
  const [scrolled, setScrolled] = useState(false);

  // スクロール検知
  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  // スムーズスクロール用関数
  const scrollToSection = (id) => {
    setIsMenuOpen(false);
    const element = document.getElementById(id);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
      setActiveSection(id);
    }
  };

  const projects = [
    {
      id: 1,
      title: "Minimalist E-Commerce",
      category: "Web Design / React",
      description: "余白を重視したアパレルブランドのECサイトデザインと実装。",
      color: "bg-stone-200"
    },
    {
      id: 2,
      title: "Finance Dashboard",
      category: "UI/UX Design",
      description: "複雑なデータを視覚的に整理し、直感的な操作を実現したダッシュボード。",
      color: "bg-zinc-800"
    },
    {
      id: 3,
      title: "Architecture Studio",
      category: "Branding / Development",
      description: "建築事務所のポートフォリオ。作品そのものを際立たせるモノクロームな構成。",
      color: "bg-neutral-400"
    }
  ];

  const skills = [
    { name: "React / Next.js", level: 90 },
    { name: "TypeScript", level: 85 },
    { name: "Tailwind CSS", level: 95 },
    { name: "UI/UX Design", level: 80 },
    { name: "Figma", level: 85 },
    { name: "Node.js", level: 70 },
  ];

  return (
    <div className="min-h-screen bg-white text-zinc-900 font-sans selection:bg-zinc-900 selection:text-white">
      
      {/* Navigation */}
      <nav className={`fixed top-0 left-0 w-full z-50 transition-all duration-300 ${scrolled ? 'bg-white/90 backdrop-blur-md py-4 border-b border-zinc-100' : 'bg-transparent py-8'}`}>
        <div className="container mx-auto px-6 md:px-12 flex justify-between items-center">
          <div 
            className="text-xl font-bold tracking-tighter cursor-pointer z-50"
            onClick={() => scrollToSection('home')}
          >
            PORTFOLIO.
          </div>

          {/* Desktop Menu */}
          <div className="hidden md:flex space-x-12 text-sm font-medium tracking-wide">
            {['Work', 'About', 'Contact'].map((item) => (
              <button 
                key={item}
                onClick={() => scrollToSection(item.toLowerCase())}
                className="hover:text-zinc-500 transition-colors relative group"
              >
                {item}
                <span className="absolute -bottom-1 left-0 w-0 h-px bg-zinc-900 transition-all duration-300 group-hover:w-full"></span>
              </button>
            ))}
          </div>

          {/* Mobile Menu Button */}
          <button 
            className="md:hidden z-50 p-2 focus:outline-none"
            onClick={() => setIsMenuOpen(!isMenuOpen)}
          >
            {isMenuOpen ? <IconX className="w-6 h-6" /> : <IconMenu className="w-6 h-6" />}
          </button>

          {/* Mobile Menu Overlay */}
          <div className={`fixed inset-0 bg-white z-40 flex flex-col justify-center items-center space-y-8 transition-all duration-500 transform ${isMenuOpen ? 'opacity-100 translate-y-0' : 'opacity-0 -translate-y-full pointer-events-none'}`}>
            {['Home', 'Work', 'About', 'Contact'].map((item) => (
              <button 
                key={item}
                onClick={() => scrollToSection(item.toLowerCase())}
                className="text-3xl font-light tracking-tighter hover:text-zinc-500 transition-colors"
              >
                {item}
              </button>
            ))}
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section id="home" className="min-h-screen flex items-center justify-center px-6 pt-20">
        <div className="max-w-5xl w-full space-y-8">
          <p className="text-zinc-500 tracking-widest text-sm uppercase animate-fade-in-up">Web Developer & Designer</p>
          <h1 className="text-5xl md:text-8xl font-bold tracking-tighter leading-[1.1] md:leading-[1.1]">
            Creating digital <br />
            <span className="text-zinc-400">experiences</span> with <br />
            simplicity & purpose.
          </h1>
          <div className="pt-8 flex items-center space-x-4">
            <button 
              onClick={() => scrollToSection('work')}
              className="group flex items-center space-x-2 bg-zinc-900 text-white px-8 py-4 rounded-full hover:bg-zinc-800 transition-all"
            >
              <span>View Projects</span>
              <IconArrowRight className="w-4 h-4 group-hover:translate-x-1 transition-transform" />
            </button>
            <div className="h-px w-16 bg-zinc-200"></div>
            <span className="text-xs text-zinc-400 tracking-wide">SCROLL DOWN</span>
          </div>
        </div>
      </section>

      {/* Work Section */}
      <section id="work" className="py-24 px-6 md:px-12 bg-zinc-50">
        <div className="container mx-auto max-w-6xl">
          <div className="flex flex-col md:flex-row justify-between items-end mb-16">
            <h2 className="text-4xl font-bold tracking-tighter">Selected Works</h2>
            <p className="text-zinc-500 mt-4 md:mt-0 max-w-sm text-sm leading-relaxed">
              デザインと機能性を兼ね備えた、最近のプロジェクトの一部をご紹介します。
            </p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 gap-x-10 gap-y-16">
            {projects.map((project) => (
              <div key={project.id} className="group cursor-pointer">
                {/* Project Thumbnail Placeholder */}
                <div className={`w-full aspect-[4/3] ${project.color} mb-6 overflow-hidden relative`}>
                   <div className="absolute inset-0 bg-black/0 group-hover:bg-black/5 transition-colors duration-500"></div>
                   {/* Decorative element inside placeholder */}
                   <div className="absolute bottom-6 right-6 opacity-0 group-hover:opacity-100 transition-all duration-500 transform translate-y-4 group-hover:translate-y-0">
                     <div className="bg-white p-3 rounded-full shadow-lg">
                       <IconExternalLink className="w-5 h-5 text-black" />
                     </div>
                   </div>
                </div>
                
                <div className="flex justify-between items-start">
                  <div>
                    <h3 className="text-xl font-bold tracking-tight group-hover:text-zinc-600 transition-colors">{project.title}</h3>
                    <p className="text-zinc-400 text-sm mt-1">{project.category}</p>
                  </div>
                  <span className="text-xs font-medium border border-zinc-200 px-3 py-1 rounded-full text-zinc-500">2024</span>
                </div>
                <p className="mt-3 text-zinc-600 text-sm leading-relaxed text-justify">
                  {project.description}
                </p>
              </div>
            ))}
          </div>
          
          <div className="mt-20 text-center">
             <button className="text-sm font-medium border-b border-zinc-900 pb-1 hover:text-zinc-600 hover:border-zinc-600 transition-colors">
               View All Archives
             </button>
          </div>
        </div>
      </section>

      {/* About & Skills Section */}
      <section id="about" className="py-24 px-6 md:px-12">
        <div className="container mx-auto max-w-6xl">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-16">
            
            {/* About Text */}
            <div className="space-y-8">
              <h2 className="text-4xl font-bold tracking-tighter">About Me</h2>
              <p className="text-zinc-600 leading-loose text-justify">
                東京を拠点に活動するWebデベロッパー兼UIデザイナーです。
                「機能的な美しさ」を追求し、ユーザーにとって直感的でありながら、
                視覚的にも心地よいデジタル体験を構築することを大切にしています。
                コードを書くことと同じくらい、タイポグラフィやレイアウトの細部を調整することに情熱を注いでいます。
              </p>
              <p className="text-zinc-600 leading-loose text-justify">
                新しい技術の習得には常に貪欲で、最近は3Dグラフィックスやインタラクティブな
                Webアニメーションの実装に力を入れています。
              </p>
              
              <div className="pt-4">
                <h4 className="font-bold mb-4 text-sm uppercase tracking-widest">Connect</h4>
                <div className="flex space-x-4">
                  <a href="#" className="p-3 bg-zinc-50 rounded-full hover:bg-zinc-100 transition-colors"><IconGithub className="w-5 h-5" /></a>
                  <a href="#" className="p-3 bg-zinc-50 rounded-full hover:bg-zinc-100 transition-colors"><IconTwitter className="w-5 h-5" /></a>
                </div>
              </div>
            </div>

            {/* Skills List */}
            <div className="bg-zinc-50 p-8 md:p-12 rounded-2xl">
              <h3 className="text-xl font-bold mb-8 tracking-tight">Technical Skills</h3>
              <div className="space-y-6">
                {skills.map((skill) => (
                  <div key={skill.name}>
                    <div className="flex justify-between mb-2">
                      <span className="font-medium text-sm">{skill.name}</span>
                      <span className="text-zinc-400 text-xs">{skill.level}%</span>
                    </div>
                    <div className="h-2 w-full bg-zinc-200 rounded-full overflow-hidden">
                      <div 
                        className="h-full bg-zinc-800 rounded-full"
                        style={{ width: `${skill.level}%` }}
                      ></div>
                    </div>
                  </div>
                ))}
              </div>
              <div className="mt-10 pt-8 border-t border-zinc-200">
                 <div className="flex flex-wrap gap-3">
                    {['VS Code', 'Git', 'Notion', 'Adobe CC', 'Blender'].map(tool => (
                        <span key={tool} className="text-xs text-zinc-500 bg-white px-3 py-1 rounded border border-zinc-100 shadow-sm">{tool}</span>
                    ))}
                 </div>
              </div>
            </div>

          </div>
        </div>
      </section>

      {/* Contact Section */}
      <section id="contact" className="py-24 px-6 md:px-12 bg-zinc-900 text-white">
        <div className="container mx-auto max-w-4xl text-center">
          <p className="text-zinc-400 text-sm tracking-widest uppercase mb-6">Got a project?</p>
          <h2 className="text-5xl md:text-7xl font-bold tracking-tighter mb-10">Let's work together.</h2>
          <p className="text-zinc-400 max-w-lg mx-auto mb-12 leading-relaxed">
            お仕事のご依頼やご相談、その他のお問い合わせはこちらから。
            3営業日以内に返信いたします。
          </p>
          
          <a 
            href="mailto:hello@example.com"
            className="inline-flex items-center space-x-3 bg-white text-zinc-900 px-8 py-4 rounded-full font-bold hover:bg-zinc-200 transition-colors"
          >
            <IconMail className="w-5 h-5" />
            <span>hello@example.com</span>
          </a>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-8 px-6 border-t border-zinc-100 text-center">
        <p className="text-xs text-zinc-400 font-medium tracking-wide">
          © 2024 PORTFOLIO. ALL RIGHTS RESERVED.
        </p>
      </footer>

      {/* Global CSS for specific animations/fonts */}
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&family=Noto+Sans+JP:wght@300;400;500;700&display=swap');
        
        body {
          font-family: 'Inter', 'Noto Sans JP', sans-serif;
        }
        
        .animate-fade-in-up {
          animation: fadeInUp 1s ease-out forwards;
        }
        
        @keyframes fadeInUp {
          from {
            opacity: 0;
            transform: translateY(20px);
          }
          to {
            opacity: 1;
            transform: translateY(0);
          }
        }
      `}</style>
    </div>
  );
}# portfolio-1
