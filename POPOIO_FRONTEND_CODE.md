# Popoio - Frontend Code (Pages & Components)

## Pages

### `client/src/pages/home.tsx`
```tsx
import { useState, useEffect } from "react";
import { Navbar } from "@/components/ui/navbar";
import { Footer } from "@/components/ui/footer";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardHeader, CardTitle, CardFooter } from "@/components/ui/card";
import { BarChart3, Users, Bell, CheckCircle2, Stethoscope, Eye, Activity, FileSpreadsheet, Zap, Shield, Smartphone, Check, TrendingUp, UserMinus, Sparkles, Footprints } from "lucide-react";
import { ContactFormDialog } from "@/components/contact-form-dialog";

import heroVideo from "@assets/generated_videos/abstract_medical_technology_waves_in_teal_and_cream.mp4";
import clinicVideo from "@assets/generated_videos/cinematic_pan_of_a_modern_dental_clinic_reception.mp4";
import dashboardVideo from "@assets/generated_videos/futuristic_medical_dashboard_interface_with_teal_glow.mp4";
import doctorVideo from "@assets/generated_videos/doctor_using_futuristic_tablet_interface.mp4";
import crmVideo from "@assets/generated_videos/clean_patient_list_scrolling_on_tablet.mp4";
import alertsVideo from "@assets/generated_videos/smartphone_receiving_medical_appointment_notification.mp4";

const stats = [
  { label: "Eficiencia", value: "+45%", icon: Zap, isPositive: true },
  { label: "Conversion", value: "+15%", icon: TrendingUp, isPositive: true },
  { label: "No-Show", value: "-25%", icon: UserMinus, isPositive: false },
];

const testimonials = [
  {
    quote: "Es la primera vez que disfruto usando un software de gestion. Es fluido, rapido y visualmente relajante.",
    author: "Dr. Marcos Ruiz",
    role: "Director Medico, Clinica Ruiz",
    image: "https://randomuser.me/api/portraits/men/32.jpg"
  },
  {
    quote: "Desde que usamos Popoio, hemos optimizado todos nuestros procesos. La mejor inversion del ano.",
    author: "Dra. Leire Boccio",
    role: "Clinica Leire Boccio",
    image: "https://randomuser.me/api/portraits/women/44.jpg"
  },
  {
    quote: "La interfaz es tan intuitiva que mi equipo aprendio a usarla en una tarde. Soporte de 10.",
    author: "Dr. Javier M.",
    role: "Centro de Estetica Avanzada",
    image: "https://randomuser.me/api/portraits/men/64.jpg"
  }
];

export default function Home() {
  const [statIndex, setStatIndex] = useState(0);
  const [testimonialIndex, setTestimonialIndex] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setStatIndex((prev) => (prev + 1) % stats.length);
    }, 3000);
    return () => clearInterval(interval);
  }, []);

  useEffect(() => {
    const interval = setInterval(() => {
      setTestimonialIndex((prev) => (prev + 1) % testimonials.length);
    }, 5000);
    return () => clearInterval(interval);
  }, []);

  const currentStat = stats[statIndex];
  const currentTestimonial = testimonials[testimonialIndex];

  return (
    <div className="min-h-screen bg-background font-sans selection:bg-primary/20 overflow-x-hidden">
      <Navbar />
      
      <main>
        <section className="relative pt-20 pb-16 md:pt-32 md:pb-24 overflow-hidden">
          <div className="container mx-auto px-4 grid md:grid-cols-2 gap-12 items-center">
            <div className="space-y-8 animate-in fade-in slide-in-from-bottom-8 duration-1000 relative z-10">
              <div className="inline-flex items-center rounded-full border border-primary/20 bg-primary/5 px-3 py-1 text-sm font-medium text-primary backdrop-blur-sm">
                <span className="flex h-2 w-2 rounded-full bg-primary mr-2 animate-pulse"></span>
                La solucion digital del futuro
              </div>
              <h1 className="text-5xl md:text-7xl font-bold tracking-tight text-foreground leading-[1.1]">
                Tu clinica, <br/>
                <span className="text-transparent bg-clip-text bg-gradient-to-r from-primary to-teal-400">version 2.0</span>
              </h1>
              <p className="text-lg text-muted-foreground max-w-lg leading-relaxed">
                Popoio simplifica la gestion digital con tecnologia de vanguardia. Paneles de control inteligentes y alertas automaticas en una experiencia visual increible.
              </p>
              <div className="flex flex-col sm:flex-row gap-4">
                <ContactFormDialog>
                  <Button size="lg" className="rounded-full text-base px-8 h-14 bg-primary hover:bg-primary/90 text-white shadow-xl hover:shadow-2xl hover:shadow-primary/20 transition-all hover:-translate-y-1 w-full sm:w-auto">
                    Empezar Ahora
                  </Button>
                </ContactFormDialog>
              </div>
            </div>
            
            <div className="relative animate-in fade-in slide-in-from-right-8 duration-1000 delay-200 group perspective-1000">
              <div className="absolute -inset-10 bg-gradient-to-r from-primary/30 to-secondary/60 rounded-full blur-[100px] opacity-60 -z-10 animate-pulse-slow" />
              <div className="relative rounded-[2rem] overflow-hidden shadow-2xl border-[6px] border-white/80 transform md:rotate-y-12 md:rotate-x-6 group-hover:rotate-0 transition-transform duration-700 ease-out">
                 <video 
                  autoPlay 
                  loop 
                  muted 
                  playsInline
                  className="w-full h-full object-cover aspect-video scale-105"
                 >
                    <source src={heroVideo} type="video/mp4" />
                 </video>
                
                <div className="absolute bottom-6 left-6 right-6">
                  <div className="bg-white/90 backdrop-blur-md p-4 rounded-2xl shadow-lg border border-white/50 flex items-center gap-4 transform translate-y-2 hover:translate-y-0 transition-transform">
                    <div className="p-3 bg-primary/10 rounded-xl text-primary transition-all duration-500 key={currentStat.label}">
                      <currentStat.icon className="h-6 w-6 fill-current" />
                    </div>
                    <div className="min-w-[120px]">
                      <div className="text-sm font-medium text-muted-foreground animate-in fade-in slide-in-from-bottom-2 duration-300 key={currentStat.label}-label">
                        {currentStat.label}
                      </div>
                      <div className={`text-2xl font-bold animate-in fade-in slide-in-from-bottom-2 duration-300 delay-75 ${currentStat.isPositive ? 'text-green-600' : 'text-red-600'} key={currentStat.label}-value`}>
                        {currentStat.value}
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section id="soluciones" className="py-24 relative bg-white">
          <div className="container mx-auto px-4 relative z-10">
            <div className="text-center max-w-3xl mx-auto mb-20 space-y-4">
              <h2 className="text-4xl md:text-5xl font-bold text-foreground tracking-tight">Tecnologia que se siente magica</h2>
              <p className="text-xl text-muted-foreground">
                Herramientas potentes envueltas en una interfaz que da gusto usar.
              </p>
            </div>

            <div className="grid md:grid-cols-3 gap-8">
              <div className="md:col-span-2 relative group rounded-3xl overflow-hidden shadow-xl min-h-[300px]">
                <video 
                  autoPlay 
                  loop 
                  muted 
                  playsInline
                  className="absolute inset-0 w-full h-full object-cover opacity-90 group-hover:scale-105 transition-transform duration-700"
                >
                  <source src={dashboardVideo} type="video/mp4" />
                </video>
                <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent" />
                <div className="absolute bottom-0 left-0 p-8">
                  <div className="w-12 h-12 rounded-2xl bg-white/10 backdrop-blur-md flex items-center justify-center mb-4 border border-white/20">
                    <BarChart3 className="h-6 w-6 text-white" />
                  </div>
                  <h3 className="text-2xl font-bold text-white mb-2">Paneles de Control en Tiempo Real</h3>
                  <p className="text-white/80 max-w-md">
                    Visualiza el pulso de tu clinica con graficos animados y datos en vivo. Toma el control total.
                  </p>
                </div>
              </div>

              <Card className="group border-none shadow-xl bg-secondary/30 hover:bg-secondary/50 transition-colors duration-300 rounded-3xl flex flex-col justify-between relative overflow-hidden">
                <div className="absolute inset-0 opacity-0 group-hover:opacity-20 transition-opacity duration-700">
                    <video autoPlay loop muted playsInline className="w-full h-full object-cover">
                        <source src={crmVideo} type="video/mp4" />
                    </video>
                </div>
                <CardHeader className="relative z-10">
                  <div className="w-14 h-14 rounded-2xl bg-primary text-white flex items-center justify-center mb-2 shadow-lg shadow-primary/30 group-hover:rotate-12 transition-transform">
                    <Users className="h-7 w-7" />
                  </div>
                  <CardTitle className="text-2xl">CRM Intuitivo</CardTitle>
                </CardHeader>
                <CardContent className="relative z-10">
                  <p className="text-muted-foreground text-lg">
                    Gestiona pacientes como si usaras tu app favorita. Simple, rapido y bonito.
                  </p>
                </CardContent>
              </Card>

              <Card className="group border-none shadow-xl bg-white border border-border/50 hover:border-primary/50 transition-all duration-300 rounded-3xl relative overflow-hidden">
                 <div className="absolute inset-0 opacity-0 group-hover:opacity-20 transition-opacity duration-700">
                    <video autoPlay loop muted playsInline className="w-full h-full object-cover">
                        <source src={alertsVideo} type="video/mp4" />
                    </video>
                </div>
                <CardHeader className="relative z-10">
                  <div className="w-14 h-14 rounded-2xl bg-teal-100 text-teal-600 flex items-center justify-center mb-2 group-hover:scale-110 transition-transform">
                    <Bell className="h-7 w-7" />
                  </div>
                  <CardTitle className="text-2xl">Alertas Smart</CardTitle>
                </CardHeader>
                <CardContent className="relative z-10">
                  <p className="text-muted-foreground text-lg">
                    WhatsApp y Email automaticos. Tus pacientes nunca olvidaran una cita.
                  </p>
                </CardContent>
              </Card>

              <div className="md:col-span-2 bg-foreground text-background rounded-3xl p-8 relative overflow-hidden group">
                <div className="absolute top-0 right-0 -mt-10 -mr-10 w-64 h-64 bg-primary/20 rounded-full blur-3xl group-hover:bg-primary/30 transition-colors" />
                <div className="relative z-10 flex flex-col md:flex-row items-center gap-8">
                  <div className="flex-1">
                     <div className="inline-flex items-center rounded-full border border-white/20 bg-white/10 px-3 py-1 text-sm font-medium text-white mb-4">
                        <FileSpreadsheet className="w-4 h-4 mr-2" />
                        Data Freedom
                      </div>
                    <h3 className="text-3xl font-bold mb-4">Tu Excel de siempre</h3>
                    <p className="text-white/70 text-lg mb-6">
                      Sin ataduras. Descarga todos tus datos y trabaja como siempre has hecho. Compatibilidad total 100%.
                    </p>
                    <Button variant="secondary" className="rounded-full">
                      Exportar Demo
                    </Button>
                  </div>
                  <div className="w-full md:w-1/3">
                     <div className="grid grid-cols-3 gap-2 opacity-50">
                        {[...Array(9)].map((_, i) => (
                            <div key={i} className="h-12 rounded-lg bg-white/10 animate-pulse" style={{animationDelay: `${i * 100}ms`}} />
                        ))}
                     </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section className="py-0 overflow-hidden">
            <div className="relative h-[60vh] min-h-[500px] w-full">
                <video 
                  autoPlay 
                  loop 
                  muted 
                  playsInline
                  className="absolute inset-0 w-full h-full object-cover"
                >
                  <source src={doctorVideo} type="video/mp4" />
                </video>
                <div className="absolute inset-0 bg-primary/80 mix-blend-multiply" />
                <div className="absolute inset-0 bg-gradient-to-r from-black/80 to-transparent" />
                
                <div className="container mx-auto px-4 h-full flex items-center relative z-10">
                    <div className="max-w-2xl text-white">
                        <h2 className="text-4xl md:text-6xl font-bold mb-6 leading-tight">
                            Tecnologia humana para <br/>profesionales reales.
                        </h2>
                        <div className="relative min-h-[140px]">
                          <p className="text-xl opacity-90 mb-8 font-light italic animate-in fade-in slide-in-from-bottom-4 duration-500 key={currentTestimonial.quote}">
                              "{currentTestimonial.quote}"
                          </p>
                        </div>
                        <div className="flex items-center gap-4 animate-in fade-in duration-700">
                            <div className="w-16 h-16 rounded-full border-2 border-white/30 overflow-hidden p-1">
                                <img src={currentTestimonial.image} alt="Doctor" className="rounded-full w-full h-full object-cover" />
                            </div>
                            <div>
                                <div className="font-bold text-lg">{currentTestimonial.author}</div>
                                <div className="text-sm opacity-70">{currentTestimonial.role}</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="precios" className="py-24 bg-secondary/10 relative">
          <div className="container mx-auto px-4">
             <div className="text-center max-w-3xl mx-auto mb-16 space-y-4">
              <h2 className="text-3xl md:text-4xl font-bold text-foreground">Planes simples y transparentes</h2>
              <p className="text-lg text-muted-foreground">
                Invierte en el crecimiento de tu clinica con tarifas claras.
              </p>
            </div>

            <div className="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
              <Card className="border-none shadow-xl bg-white rounded-3xl relative overflow-hidden flex flex-col">
                <div className="h-2 bg-primary w-full absolute top-0 left-0" />
                <CardHeader className="pb-4">
                   <h3 className="text-xl font-bold text-muted-foreground uppercase tracking-wider">Plan Basico</h3>
                   <div className="mt-4 flex items-baseline">
                     <span className="text-5xl font-bold text-foreground">600EUR</span>
                     <span className="ml-2 text-muted-foreground">/mes</span>
                   </div>
                   <p className="text-sm text-muted-foreground mt-2">Perfecto para clinicas que estan empezando a digitalizarse.</p>
                </CardHeader>
                <CardContent className="flex-1">
                   <ul className="space-y-4 mt-4">
                      {[
                        "Gestion de hasta 500 pacientes",
                        "Agenda basica de citas",
                        "Recordatorios por Email",
                        "Panel de control estandar",
                        "Soporte por Email"
                      ].map((item, i) => (
                        <li key={i} className="flex items-center gap-3 text-sm">
                          <div className="p-1 rounded-full bg-primary/10 text-primary">
                            <Check className="h-3 w-3" />
                          </div>
                          {item}
                        </li>
                      ))}
                   </ul>
                </CardContent>
                <CardFooter className="pt-8">
                   <ContactFormDialog className="w-full">
                    <Button className="w-full rounded-full bg-primary hover:bg-primary/90 h-12 font-bold shadow-lg">
                      Empezar Ahora
                    </Button>
                   </ContactFormDialog>
                </CardFooter>
              </Card>

              <Card className="border-none shadow-xl bg-foreground text-background rounded-3xl relative overflow-hidden flex flex-col">
                <div className="absolute top-0 right-0 -mt-20 -mr-20 w-64 h-64 bg-primary/20 rounded-full blur-3xl" />
                <CardHeader className="pb-4 relative z-10">
                   <h3 className="text-xl font-bold text-primary uppercase tracking-wider">Plan Personalizado</h3>
                   <div className="mt-4 flex items-baseline">
                     <span className="text-4xl font-bold text-background">A medida</span>
                   </div>
                   <p className="text-sm text-background/70 mt-2">Para clinicas con multiples sedes o necesidades especiales.</p>
                </CardHeader>
                <CardContent className="flex-1 relative z-10">
                   <ul className="space-y-4 mt-4">
                      {[
                        "Pacientes ilimitados",
                        "Multiples doctores y agendas",
                        "Recordatorios por WhatsApp",
                        "Paneles avanzados y KPIs",
                        "Integracion con maquinaria",
                        "Soporte prioritario 24/7",
                        "Formacion al equipo"
                      ].map((item, i) => (
                        <li key={i} className="flex items-center gap-3 text-sm">
                          <div className="p-1 rounded-full bg-primary text-white">
                            <Check className="h-3 w-3" />
                          </div>
                          {item}
                        </li>
                      ))}
                   </ul>
                </CardContent>
                <CardFooter className="pt-8 relative z-10">
                   <ContactFormDialog className="w-full">
                    <Button variant="secondary" className="w-full rounded-full h-12 font-bold shadow-lg hover:scale-105 transition-transform">
                      Empezar Ahora
                    </Button>
                   </ContactFormDialog>
                </CardFooter>
              </Card>
            </div>
          </div>
        </section>

        <section id="clientes" className="py-24 bg-secondary/30 overflow-hidden">
          <div className="container mx-auto px-4">
            <div className="grid lg:grid-cols-2 gap-16 items-center">
              <div className="relative order-2 lg:order-1 group">
                <div className="absolute -inset-4 bg-gradient-to-tr from-primary to-accent rounded-[2.5rem] blur-lg opacity-30 group-hover:opacity-50 transition-opacity duration-500" />
                <div className="relative rounded-[2rem] overflow-hidden shadow-2xl border-4 border-white">
                  <video 
                    autoPlay 
                    loop 
                    muted 
                    playsInline
                    className="w-full h-full object-cover aspect-[4/3]"
                  >
                    <source src={clinicVideo} type="video/mp4" />
                  </video>
                  
                  <div className="absolute bottom-6 right-6 left-6 bg-white/80 backdrop-blur-xl p-6 rounded-2xl border border-white/40 shadow-lg">
                     <div className="flex justify-between items-end">
                        <div>
                            <p className="text-sm font-bold text-primary uppercase tracking-wider mb-1">Estado de la Clinica</p>
                            <h4 className="text-2xl font-bold text-foreground">Operativo 100%</h4>
                        </div>
                        <div className="h-10 w-10 bg-green-500 rounded-full flex items-center justify-center animate-bounce text-white">
                            <CheckCircle2 className="h-6 w-6" />
                        </div>
                     </div>
                  </div>
                </div>
              </div>

              <div className="order-1 lg:order-2 space-y-8">
                <h2 className="text-4xl md:text-5xl font-bold text-foreground">
                  Disenado para tu especialidad
                </h2>
                <p className="text-lg text-muted-foreground">
                  No importa si eres dentista, fisioterapeuta o dermatologo. Popoio se adapta como un guante.
                </p>
                
                <div className="grid sm:grid-cols-2 gap-4">
                    {[
                        { icon: CheckCircle2, title: "Dental", desc: "Odontogramas 3D" },
                        { icon: Eye, title: "Oftalmologia", desc: "Graduacion visual" },
                        { icon: Sparkles, title: "Estetica", desc: "Seguimiento fotografico" },
                        { icon: Activity, title: "Fisioterapia", desc: "Evolucion grafica" },
                        { icon: Footprints, title: "Podologia", desc: "Estudios de pisada" },
                        { icon: Stethoscope, title: "Medicina General", desc: "Historial unificado" },
                    ].map((item, i) => (
                        <div key={i} className="flex items-start gap-3 p-4 rounded-xl bg-white border border-border/50 hover:border-primary/50 hover:shadow-md transition-all cursor-default">
                            <div className="p-2 rounded-lg bg-primary/10 text-primary">
                                <item.icon className="h-5 w-5" />
                            </div>
                            <div>
                                <h3 className="font-semibold text-foreground">{item.title}</h3>
                                <p className="text-xs text-muted-foreground">{item.desc}</p>
                            </div>
                        </div>
                    ))}
                </div>
              </div>
            </div>
          </div>
        </section>

        <section className="py-32 bg-foreground text-background relative overflow-hidden">
          <div className="absolute inset-0 overflow-hidden">
             <div className="absolute -top-[50%] -right-[20%] w-[80vw] h-[80vw] rounded-full bg-primary/20 blur-[120px] animate-pulse-slow" />
             <div className="absolute -bottom-[50%] -left-[20%] w-[80vw] h-[80vw] rounded-full bg-secondary/10 blur-[120px]" />
          </div>
          
          <div className="container mx-auto px-4 text-center relative z-10">
            <h2 className="text-4xl md:text-6xl font-bold mb-8 tracking-tighter">Listo para el siguiente nivel?</h2>
            <p className="text-background/70 text-xl max-w-2xl mx-auto mb-12 font-light">
              Deja atras el papel y el software de los 90. <br/>Bienvenido al futuro de la gestion clinica.
            </p>
            <div className="flex flex-col sm:flex-row gap-6 justify-center">
              <ContactFormDialog>
                <Button size="lg" className="rounded-full bg-primary text-white font-bold text-lg px-10 h-16 shadow-2xl shadow-primary/30 hover:scale-105 transition-transform">
                  Empezar Ahora
                </Button>
              </ContactFormDialog>
            </div>
            <p className="mt-8 text-sm text-background/40">Sin tarjeta de credito - Cancelacion en cualquier momento</p>
          </div>
        </section>
      </main>

      <Footer />
    </div>
  );
}
```

---

### `client/src/pages/blog.tsx`
```tsx
import { useEffect, useState } from "react";
import { Link } from "wouter";
import { Navbar } from "@/components/ui/navbar";
import { Footer } from "@/components/ui/footer";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Calendar, Clock, Tag } from "lucide-react";
import type { BlogArticle } from "@shared/schema";

export default function Blog() {
  const [articles, setArticles] = useState<BlogArticle[]>([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    document.title = "Blog - Popoio | Transformacion Digital para Clinicas Medicas";
    
    const metaDescription = document.querySelector('meta[name="description"]');
    if (metaDescription) {
      metaDescription.setAttribute("content", "Articulos sobre transformacion digital, gestion de clinicas medicas, reduccion de no-shows y tecnologia sanitaria. Consejos practicos para modernizar tu clinica.");
    }
  }, []);

  useEffect(() => {
    async function fetchArticles() {
      try {
        const response = await fetch("/api/blog");
        const data = await response.json();
        setArticles(data);
      } catch (error) {
        console.error("Error fetching blog articles:", error);
      } finally {
        setLoading(false);
      }
    }
    fetchArticles();
  }, []);

  const formatDate = (dateString: Date | string) => {
    const date = new Date(dateString);
    return date.toLocaleDateString('es-ES', { year: 'numeric', month: 'long', day: 'numeric' });
  };

  const estimateReadingTime = (content: string) => {
    const wordsPerMinute = 200;
    const words = content.replace(/<[^>]*>/g, '').split(/\s+/).length;
    return Math.ceil(words / wordsPerMinute);
  };

  return (
    <div className="min-h-screen bg-background">
      <Navbar />
      
      <main className="pt-24 pb-16">
        <div className="container mx-auto px-4">
          <div className="max-w-4xl mx-auto text-center mb-16">
            <div className="inline-flex items-center rounded-full border border-primary/20 bg-primary/5 px-3 py-1 text-sm font-medium text-primary backdrop-blur-sm mb-6">
              <span className="flex h-2 w-2 rounded-full bg-primary mr-2 animate-pulse"></span>
              Blog de Transformacion Digital
            </div>
            <h1 className="text-4xl md:text-6xl font-bold tracking-tight text-foreground mb-6">
              Aprende a <span className="text-transparent bg-clip-text bg-gradient-to-r from-primary to-teal-400">modernizar</span> tu clinica
            </h1>
            <p className="text-xl text-muted-foreground max-w-2xl mx-auto">
              Guias practicas, casos de exito y estrategias probadas para llevar tu clinica medica al siguiente nivel digital.
            </p>
          </div>

          {loading ? (
            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
              {[1, 2, 3].map((i) => (
                <Card key={i} className="animate-pulse">
                  <div className="h-48 bg-gray-200 rounded-t-lg" />
                  <CardHeader>
                    <div className="h-6 bg-gray-200 rounded w-3/4 mb-4" />
                    <div className="h-4 bg-gray-200 rounded w-full mb-2" />
                    <div className="h-4 bg-gray-200 rounded w-2/3" />
                  </CardHeader>
                </Card>
              ))}
            </div>
          ) : (
            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
              {articles.map((article) => (
                <Link key={article.id} href={`/blog/${article.slug}`} data-testid={`link-article-${article.slug}`}>
                  <Card 
                    className="h-full hover:shadow-xl transition-all duration-300 cursor-pointer group border-none shadow-lg hover:-translate-y-1"
                    data-testid={`card-article-${article.id}`}
                  >
                    <div className="h-48 bg-gradient-to-br from-primary/20 to-teal-400/20 rounded-t-lg flex items-center justify-center group-hover:from-primary/30 group-hover:to-teal-400/30 transition-all">
                      <div className="text-6xl">
                        {article.tags?.[0]?.includes('digital') ? '🚀' :
                         article.tags?.[0]?.includes('no-show') ? '📅' :
                         article.tags?.[0]?.includes('CRM') ? '💻' : '📊'}
                      </div>
                    </div>
                    <CardHeader>
                      <div className="flex items-center gap-2 text-xs text-muted-foreground mb-3">
                        <Calendar className="h-3 w-3" />
                        <span>{formatDate(article.publishedAt)}</span>
                        <span>-</span>
                        <Clock className="h-3 w-3" />
                        <span>{estimateReadingTime(article.content)} min lectura</span>
                      </div>
                      <CardTitle className="text-xl leading-tight group-hover:text-primary transition-colors">
                        {article.title}
                      </CardTitle>
                    </CardHeader>
                    <CardContent>
                      <p className="text-muted-foreground text-sm leading-relaxed mb-4">
                        {article.excerpt}
                      </p>
                      {article.tags && article.tags.length > 0 && (
                        <div className="flex flex-wrap gap-2">
                          {article.tags.slice(0, 3).map((tag, idx) => (
                            <span 
                              key={idx} 
                              className="inline-flex items-center gap-1 px-2 py-1 rounded-full bg-primary/10 text-primary text-xs"
                            >
                              <Tag className="h-3 w-3" />
                              {tag}
                            </span>
                          ))}
                        </div>
                      )}
                    </CardContent>
                  </Card>
                </Link>
              ))}
            </div>
          )}

          {!loading && articles.length === 0 && (
            <div className="text-center py-16">
              <p className="text-muted-foreground text-lg">No hay articulos disponibles en este momento.</p>
            </div>
          )}
        </div>
      </main>

      <Footer />
    </div>
  );
}
```

---

### `client/src/pages/blog-article.tsx`
Copia directamente del archivo actual en el proyecto (232 lineas). Incluye DOMPurify para sanitizar HTML, JSON-LD structured data, y los botones de compartir y volver al blog.

### `client/src/pages/faq.tsx`
Copia directamente del archivo actual en el proyecto (177 lineas). Incluye buscador, accordion por categorias, y JSON-LD FAQPage schema.

### `client/src/pages/dashboard.tsx`
Copia directamente del archivo actual en el proyecto (213 lineas). Panel de control mockup con sidebar, stats cards, y lista de citas.

### `client/src/pages/login.tsx`
Copia directamente del archivo actual en el proyecto (83 lineas). Pagina de login con formulario simulado.

### `client/src/pages/not-found.tsx`
```tsx
import { Card, CardContent } from "@/components/ui/card";
import { AlertCircle } from "lucide-react";

export default function NotFound() {
  return (
    <div className="min-h-screen w-full flex items-center justify-center bg-gray-50">
      <Card className="w-full max-w-md mx-4">
        <CardContent className="pt-6">
          <div className="flex mb-4 gap-2">
            <AlertCircle className="h-8 w-8 text-red-500" />
            <h1 className="text-2xl font-bold text-gray-900">404 Page Not Found</h1>
          </div>
          <p className="mt-4 text-sm text-gray-600">
            Did you forget to add the page to the router?
          </p>
        </CardContent>
      </Card>
    </div>
  );
}
```

---

## Components

### `client/src/components/contact-form-dialog.tsx`
Copia directamente del archivo actual (168 lineas). Formulario de contacto con Dialog, validacion Zod, y envio POST a /api/contact.

### `client/src/components/ui/navbar.tsx`
Copia directamente del archivo actual (37 lineas). Navbar con logo, links de navegacion, y boton CTA.

### `client/src/components/ui/footer.tsx`
Copia directamente del archivo actual (58 lineas). Footer con logo, links y copyright.

### UI Components (shadcn/ui)
Los siguientes son componentes estandar de shadcn/ui estilo "new-york". Puedes regenerarlos con:
```bash
npx shadcn@latest add accordion button card dialog form input label toast tooltip
```
O copiarlos directamente del proyecto:
- `accordion.tsx`, `button.tsx`, `card.tsx`, `dialog.tsx`, `form.tsx`, `input.tsx`, `label.tsx`, `toast.tsx`, `toaster.tsx`, `tooltip.tsx`

### Hooks
- `client/src/hooks/use-toast.ts` - Copia directamente (191 lineas)
- `client/src/hooks/use-mobile.tsx` - Copia directamente (19 lineas)
