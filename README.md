# chapter3
📁 Struktur Folder
chapter3/
│── app/
│   └── page.tsx
│
│── components/
│   ├── AlertBox.tsx
│   └── CustomButton.tsx
│
│── public/
│
└── tsconfig.json

🟦 AlertBox Component

Komponen ini menampilkan empat tipe alert:

Info

Success

Warning

Danger
File: components/AlertBox.tsx

type AlertType = "info" | "success" | "warning" | "danger";

interface AlertProps {
  title: string;
  message: string;
  type: AlertType;
}

export default function AlertBox({ title, message, type }: AlertProps) {
  const colors: Record<AlertType, string> = {
    info: "bg-blue-500",
    success: "bg-green-500",
    warning: "bg-yellow-500",
    danger: "bg-red-500",
  };

  return (
    <div className={`p-4 rounded-lg shadow-lg text-white ${colors[type]}`}>
      <h3 className="text-lg font-bold">{title}</h3>
      <p className="text-sm">{message}</p>
    </div>
  );
}
CustomButton Component

Tombol telah dimodifikasi menjadi lebih menarik dan memiliki beberapa variasi:

Primary

Success

Warning

Danger

Outline

📌 File: components/CustomButton.tsx

type ButtonType =
  | "primary"
  | "success"
  | "warning"
  | "danger"
  | "outline";

interface ButtonProps {
  label: string;
  type?: ButtonType;
  onClick?: () => void;
}

export default function CustomButton({
  label,
  type = "primary",
  onClick,
}: ButtonProps) {
  const styles: Record<ButtonType, string> = {
    primary: "bg-blue-600 hover:bg-blue-700 text-white",
    success: "bg-green-600 hover:bg-green-700 text-white",
    warning: "bg-yellow-500 hover:bg-yellow-600 text-black",
    danger: "bg-red-600 hover:bg-red-700 text-white",
    outline:
      "border-2 border-white text-white hover:bg-white hover:text-black",
  };

  return (
    <button
      onClick={onClick}
      className={`px-5 py-2 rounded-xl font-semibold transition-all duration-200 shadow-md hover:shadow-xl ${styles[type]}`}
    >
      {label}
    </button>
  );
}

Halaman Utama

Halaman utama menampilkan:

Alert (info, success, warning, danger)

Tombol modifikasi

📌 File: app/page.tsx

"use client";

import AlertBox from "@/components/AlertBox";
import CustomButton from "@/components/CustomButton";

export default function Home() {
  return (
    <div className="min-h-screen p-10 bg-gray-900 text-white flex flex-col gap-10">

      {/* ALERT SECTION */}
      <section>
        <h2 className="text-2xl font-bold mb-4">Tugas Praktikum — Alert</h2>

        <div className="flex flex-col gap-4">
          <AlertBox type="info" title="Informasi" message="Ini adalah alert info." />
          <AlertBox type="success" title="Berhasil" message="Aksi berhasil dilakukan." />
          <AlertBox type="warning" title="Peringatan" message="Mohon berhati-hati." />
          <AlertBox type="danger" title="Bahaya" message="Terjadi kesalahan fatal." />
        </div>
      </section>

      {/* BUTTON SECTION */}
      <section>
        <h2 className="text-2xl font-bold mb-4">Tugas Praktikum — Modifikasi Tombol</h2>

        <div className="flex gap-4 flex-wrap">
          <CustomButton type="primary" label="Primary" onClick={() => alert("Primary clicked")} />
          <CustomButton type="success" label="Success" onClick={() => alert("Success clicked")} />
          <CustomButton type="warning" label="Warning" onClick={() => alert("Warning clicked")} />
          <CustomButton type="danger" label="Danger" onClick={() => alert("Danger clicked")} />
          <CustomButton type="outline" label="Outline" onClick={() => alert("Outline clicked")} />
        </div>
      </section>
    </div>
  );
}


