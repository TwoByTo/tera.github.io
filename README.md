# tera.github.io

import { Canvas, useFrame } from '@react-three/fiber'
import { Float, OrbitControls, Environment, ContactShadows } from '@react-three/drei'
import { useRef, useState } from 'react'
import { MessageCircle, CalendarCheck, CreditCard, UtensilsCrossed, Plane, Bike, Mic } from 'lucide-react'

function TeraCube(props) {
  const ref = useRef()
  const [hovered, setHovered] = useState(false)
  useFrame((state, delta) => {
    ref.current.rotation.x += delta * 0.25
    ref.current.rotation.y += delta * 0.35
  })
  return (
    <Float floatIntensity={1.2} rotationIntensity={0.2} speed={2.5}>
      <mesh
        ref={ref}
        {...props}
        onPointerOver={() => setHovered(true)}
        onPointerOut={() => setHovered(false)}
        castShadow
        receiveShadow
      >
        <boxGeometry args={[1.6, 1.6, 1.6]} />
        <meshStandardMaterial
          roughness={0.2}
          metalness={0.6}
          color={hovered ? '#3B82F6' : '#2563EB'}
        />
      </mesh>
    </Float>
  )
}

function TeraOrbs() {
  return (
    <group>
      <mesh position={[2.2, 0.9, -0.8]}>
        <sphereGeometry args={[0.35, 32, 32]} />
        <meshStandardMaterial color={'#60A5FA'} metalness={0.3} roughness={0.4} />
      </mesh>
      <mesh position={[-2.1, -0.6, 0.4]}>
        <torusKnotGeometry args={[0.33, 0.11, 120, 16]} />
        <meshStandardMaterial color={'#93C5FD'} metalness={0.5} roughness={0.2} />
      </mesh>
    </group>
  )
}

export default function HelloTeraLanding() {
  return (
    <div className="min-h-screen bg-gradient-to-b from-slate-950 via-slate-900 to-slate-950 text-slate-50">
      {/* NAV */}
      <header className="sticky top-0 z-30 backdrop-blur supports-[backdrop-filter]:bg-slate-950/50">
        <div className="mx-auto max-w-7xl px-4 py-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="h-8 w-8 rounded-xl bg-gradient-to-br from-blue-500 to-indigo-600 shadow-lg shadow-blue-500/25" />
            <span className="text-xl font-semibold tracking-tight">hello<span className="text-blue-400">Tera</span>.ai</span>
          </div>
          <nav className="hidden gap-8 md:flex text-sm text-slate-300">
            <a href="#features" className="hover:text-white">Features</a>
            <a href="#how" className="hover:text-white">How it works</a>
            <a href="#contact" className="hover:text-white">Contact</a>
          </nav>
          <a href="#get" className="rounded-2xl bg-blue-600 px-4 py-2 text-sm font-medium shadow-lg shadow-blue-600/30 hover:bg-blue-500">Get started on WhatsApp</a>
        </div>
      </header>

      {/* HERO */}
      <section className="mx-auto max-w-7xl px-4 pt-12 pb-10 md:pt-20 md:pb-16">
        <div className="grid items-center gap-10 md:grid-cols-2">
          <div>
            <h1 className="text-4xl md:text-6xl font-extrabold leading-tight">
              Your 3D-native <span className="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-indigo-300">AI assistant</span> on WhatsApp
            </h1>
            <p className="mt-5 text-slate-300 text-lg md:text-xl max-w-xl">
              Tera books, pays, and schedules by reading your chats. Speak in voice notes or forward any message—Tera handles the rest.
            </p>
            <div className="mt-7 flex flex-wrap items-center gap-3">
              <a id="get" href="#contact" className="rounded-2xl bg-blue-600 px-5 py-3 font-medium shadow-lg shadow-blue-600/30 hover:bg-blue-500">Open WhatsApp</a>
              <a href="#features" className="rounded-2xl px-5 py-3 font-medium ring-1 ring-white/10 hover:bg-white/5">See features</a>
            </div>
            <div className="mt-6 flex items-center gap-4 text-sm text-slate-400">
              <div className="h-2 w-2 rounded-full bg-green-400" />
              <span>Powered by Google Gemini • End-to-end encrypted on WhatsApp</span>
            </div>
          </div>

          <div className="relative h-[420px] rounded-3xl bg-gradient-to-b from-slate-900 to-slate-950 ring-1 ring-white/10 p-2">
            <div className="absolute inset-0 rounded-3xl overflow-hidden">
              <Canvas camera={{ position: [3.2, 2.2, 4.2], fov: 50 }} shadows>
                <ambientLight intensity={0.2} />
                <directionalLight castShadow intensity={1.2} position={[5, 6, 3]} shadow-mapSize-width={1024} shadow-mapSize-height={1024} />
                <TeraCube position={[0, 0.5, 0]} />
                <TeraOrbs />
                <ContactShadows position={[0, -0.9, 0]} opacity={0.6} scale={10} blur={2.5} far={9} />
                <Environment preset="city" />
                <OrbitControls enablePan={false} enableZoom={false} autoRotate autoRotateSpeed={0.7} />
              </Canvas>
            </div>
            <div className="pointer-events-none absolute inset-x-6 bottom-6 flex items-center justify-between text-xs text-slate-400">
              <span>Drag to look • Hover to energize</span>
              <span>Realtime WebGL</span>
            </div>
          </div>
        </div>
      </section>

      {/* FEATURES */}
      <section id="features" className="mx-auto max-w-7xl px-4 py-12 md:py-20">
        <h2 className="text-2xl md:text-3xl font-bold">What Tera can do</h2>
        <p className="mt-2 text-slate-300">All from WhatsApp—no new app to download.</p>
        <div className="mt-8 grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
          <Feature icon={<MessageCircle className="h-5 w-5" />} title="Message understanding" desc="Forward chats; Tera parses details, dates, and intents automatically." />
          <Feature icon={<CalendarCheck className="h-5 w-5" />} title="Smart scheduling" desc="Checks both calendars (with permission) and proposes the best time." />
          <Feature icon={<CreditCard className="h-5 w-5" />} title="Payments" desc="Ryt Bank integration for fast, secure transfers and checkout." />
          <Feature icon={<UtensilsCrossed className="h-5 w-5" />} title="Restaurant booking" desc="Chats with venues like a real PA to secure your table." />
          <Feature icon={<Plane className="h-5 w-5" />} title="Travel & stays" desc="Search and book flights & hotels via partner APIs (Agoda, Airbnb)." />
          <Feature icon={<Bike className="h-5 w-5" />} title="Rides & delivery" desc="Grab, Uber, and food delivery—requested by natural language." />
        </div>
      </section>

      {/* HOW IT WORKS */}
      <section id="how" className="mx-auto max-w-7xl px-4 py-12 md:py-20">
        <div className="grid gap-10 md:grid-cols-2 items-center">
          <div className="rounded-3xl border border-white/10 p-6 bg-white/5">
            <div className="flex items-center gap-3 text-sm text-slate-300">
              <div className="h-8 w-8 rounded-xl bg-blue-600/30 grid place-items-center"><Mic className="h-4 w-4" /></div>
              <span>Voice notes supported</span>
            </div>
            <ol className="mt-6 space-y-4 text-slate-300">
              <li><span className="font-semibold text-white">1. Forward</span> a WhatsApp message or send a voice note.</li>
              <li><span className="font-semibold text-white">2. Confirm</span> what you want (book, pay, schedule, ask).</li>
              <li><span className="font-semibold text-white">3. Tera executes</span> and drops the confirmation back into your chat.</li>
            </ol>
            <p className="mt-6 text-xs text-slate-400">Tera uses Google Gemini to reason over unstructured chat, then calls partner APIs to complete tasks.</p>
          </div>
          <div className="relative h-[380px] rounded-3xl bg-gradient-to-br from-slate-900 to-slate-800 p-2 ring-1 ring-white/10">
            <div className="absolute inset-0 rounded-3xl overflow-hidden">
              <Canvas camera={{ position: [2.4, 1.6, 3.2], fov: 55 }}>
                <ambientLight intensity={0.3} />
                <directionalLight intensity={1.1} position={[4, 5, 2]} />
                <group position={[0, -0.5, 0]}>
                  <Float floatIntensity={1} rotationIntensity={0.3}>
                    <mesh castShadow position={[0, 0.6, 0]}>
                      <icosahedronGeometry args={[0.8, 0]} />
                      <meshStandardMaterial color={'#1D4ED8'} metalness={0.8} roughness={0.15} />
                    </mesh>
                  </Float>
                  <mesh rotation={[-Math.PI/2, 0, 0]} position={[0, -0.9, 0]}>
                    <cylinderGeometry args={[1.6, 1.6, 0.08, 64]} />
                    <meshStandardMaterial color={'#0F172A'} />
                  </mesh>
                </group>
                <ContactShadows position={[0, -1, 0]} opacity={0.5} scale={8} blur={2} far={8} />
                <Environment preset="night" />
                <OrbitControls enablePan={false} enableZoom={false} autoRotate autoRotateSpeed={0.8} />
              </Canvas>
            </div>
          </div>
        </div>
      </section>

      {/* CTA */}
      <section id="contact" className="mx-auto max-w-7xl px-4 py-16">
        <div className="rounded-3xl bg-gradient-to-r from-blue-600 to-indigo-600 p-8 md:p-12 flex flex-col md:flex-row items-center justify-between gap-8 shadow-[0_10px_40px_-12px_rgba(37,99,235,0.6)]">
          <div>
            <h3 className="text-2xl md:text-3xl font-bold">Start in seconds on WhatsApp</h3>
            <p className="mt-2 text-blue-100">Message “Hello Tera” to begin. No downloads, no setup.</p>
          </div>
          <div className="flex items-center gap-3">
            <a href="#" className="rounded-2xl bg-white text-slate-900 px-5 py-3 font-semibold hover:bg-blue-50">Open WhatsApp</a>
            <a href="#" className="rounded-2xl ring-2 ring-white/70 px-5 py-3 font-semibold text-white hover:bg-white/10">See a demo</a>
          </div>
        </div>
        <p className="mt-6 text-center text-xs text-slate-500">© {new Date().getFullYear()} HelloTera.ai · Privacy · Terms</p>
      </section>
    </div>
  )
}

function Feature({ icon, title, desc }) {
  return (
    <div className="rounded-2xl border border-white/10 bg-white/5 p-5 hover:bg-white/10 transition-colors">
      <div className="flex items-center gap-3">
        <div className="h-9 w-9 rounded-xl bg-blue-600/30 grid place-items-center text-blue-200">{icon}</div>
        <h3 className="font-semibold">{title}</h3>
      </div>
      <p className="mt-3 text-sm text-slate-300">{desc}</p>
    </div>
  )
}
