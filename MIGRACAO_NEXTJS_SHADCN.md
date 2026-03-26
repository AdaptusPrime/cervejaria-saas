# Análise de Migração: Cervejaria Asgard Pedidos
## HTML → Next.js + Shadcn UI

---

## 1. RESUMO EXECUTIVO

### Viabilidade: ✅ ALTA (100% viável)

O sistema **Cockpit de Pedidos da Cervejaria Asgard** pode ser 100% migrado para Next.js + Shadcn UI mantendo todas as 50+ funcionalidades existentes.

### Estratégia Adotada: **MONOLITO SIMPLIFICADO**

- ✅ Mínima modularidade (1 página principal + 1 API route)
- ✅ Sem múltiplas rotas de navegação
- ✅ Sem backend multi-server
- ✅ Toda lógica em um único arquivo de página
- ✅ Estado gerenciado via React Hooks (useState/useReducer)

---

## 2. INVENTÁRIO COMPLETO DE FEATURES

### 2.1 UI/UX (25 features)

| # | Feature | Complexidade | Shadcn Component |
|---|---------|--------------|------------------|
| 1 | Header Cockpit fixo | 🟢 Baixa | `Card`, `Button`, `Input` |
| 2 | Breadcrumb navegacional | 🟢 Baixa | `Breadcrumb` |
| 3 | KPI Panel dinâmico (6 cards) | 🟡 Média | `Card`, `Badge` |
| 4 | Form Wizard (seções colapsáveis) | 🟡 Média | `Collapsible`, `Card` |
| 5 | Seção: Dados do Pedido | 🟢 Baixa | `Card`, `Input`, `Select` |
| 6 | Seção: Dados do Cliente | 🟢 Baixa | `Card`, `Input`, `Select` |
| 7 | Seção: Condições de Pagamento | 🟢 Baixa | `Collapsible`, `Card` |
| 8 | Sistema de Tags (predefinidas + custom) | 🟡 Média | `Badge`, `Input`, custom |
| 9 | Tooltips de Glossário (siglas) | 🟢 Baixa | `Tooltip` |
| 10 | Segmento Canal com lógica condicional | 🟡 Média | `Select`, `Input` |
| 11 | Autocomplete de Produtos | 🟡 Média | `Command`, `Popover` |
| 12 | Autocomplete de Clientes | 🟢 Baixa | `Datalist` (nativo) |
| 13 | Autocomplete de Vendedores | 🟢 Baixa | `Datalist` (nativo) |
| 14 | Autocomplete de Cidades | 🟢 Baixa | `Datalist` (nativo) |
| 15 | Input Masks (CNPJ/CPF, CEP, Telefone) | 🟡 Média | Custom hook + `Input` |
| 16 | Sidebar Timeline de Eventos | 🟡 Média | `Card`, `ScrollArea`, `Avatar` |
| 17 | Panel de Atalhos de Teclado | 🟢 Baixa | `Card`, `Badge` |
| 18 | Tabela de Produtos (CRUD dinâmico) | 🔴 Alta | `Table`, `Button`, `Select` |
| 19 | Tabela de Equipamentos (CRUD dinâmico) | 🟡 Média | `Table`, `Button` |
| 20 | Canvas de Assinaturas (3 áreas) | 🔴 Alta | HTML5 Canvas (custom) |
| 21 | Footer Checklist com progresso | 🟢 Baixa | `Checkbox`, `Progress` |
| 22 | Drawer Assistente Inteligente | 🟡 Média | `Sheet` |
| 23 | Toast Notifications | 🟢 Baixa | `Sonner` ou `Toast` |
| 24 | Quick Jump Bar | 🟢 Baixa | `Button` |
| 25 | Responsividade completa | 🟡 Média | Tailwind + Shadcn |

### 2.2 Lógica de Negócio (15 features)

| # | Feature | Complexidade | Implementação |
|---|---------|--------------|---------------|
| 26 | Geração automática de ID de pedido | 🟢 Baixa | `useEffect` no mount |
| 27 | Cálculo automático de totais | 🟡 Média | `useMemo` + state |
| 28 | Cálculo de margem estimada | 🟢 Baixa | `useMemo` |
| 29 | Tabela de preços com multiplicadores | 🟡 Média | `useState` + handlers |
| 30 | Auto-seleção de tabela por segmento | 🟢 Baixa | `useEffect` |
| 31 | Desconto global com validação de limite | 🟡 Média | `useState` + validation |
| 32 | Operações de produto (Venda, Consignado, Troca, Permuta, Bonificação) | 🟡 Média | `Select` + conditional styling |
| 33 | Validação de CNPJ/CPF em tempo real | 🟡 Média | Custom hook |
| 34 | Validação de CEP | 🟢 Baixa | Regex |
| 35 | Cálculo de diferença de equipamentos | 🟢 Baixa | `useMemo` |
| 36 | Visibilidade condicional de data de retorno | 🟡 Média | `useEffect` + state |
| 37 | Timer de sessão (HH:MM:SS) | 🟢 Baixa | `useEffect` + `setInterval` |
| 38 | Checklist de conferência | 🟢 Baixa | `useState` + `Checkbox` |
| 39 | Timeline de eventos com timestamp | 🟡 Média | `useState` + formatters |
| 40 | Auto-save para localStorage | 🟡 Média | `useEffect` + debounce |

### 2.3 Integrações de API (5 features)

| # | Feature | API | Implementação |
|---|---------|-----|---------------|
| 41 | Busca de endereço por CEP | ViaCEP | Server Action ou fetch |
| 42 | Dados da empresa por CNPJ | BrasilAPI | Server Action ou fetch |
| 43 | Estados e cidades brasileiras | IBGE | Server Action + cache |
| 44 | Cálculo de rota/distância | OpenStreetMap/OSRM | API route ou fetch |
| 45 | Verificação de feriados | BrasilAPI | Server Action |

### 2.4 Utilitários (5 features)

| # | Feature | Complexidade |
|---|---------|--------------|
| 46 | Busca global (Ctrl+K) | 🟡 Média |
| 47 | Atalhos de teclado completos | 🟡 Média |
| 48 | Exportação JSON | 🟢 Baixa |
| 49 | Importação CSV | 🟡 Média |
| 50 | Impressão A4 com 2 vias | 🔴 Alta |

---

## 3. MATRIZ DE DECISÃO DE IMPLEMENTAÇÃO (MDI)

### 3.1 Decisões Arquiteturais

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         D1: ESTRUTURA DE PÁGINAS                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  [?] Múltiplas rotas (App Router)?                                      │
│      └── ❌ NÃO - Requisito: mínima modularidade                         │
│                                                                         │
│  [?] Single Page Application (SPA)?                                     │
│      └── ✅ SIM - Todo conteúdo em app/page.tsx                         │
│                                                                         │
│  [?] Server Components ou Client Components?                            │
│      └── 🟡 HÍBRIDO:                                                   │
│          - Layout: Server Component                                     │
│          - Page: 'use client' (necessita interatividade)               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                         D2: GERENCIAMENTO DE ESTADO                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  [?] Redux/Zustand/Jotai?                                               │
│      └── ❌ NÃO - Overkill para monolito                                │
│                                                                         │
│  [?] React Context + useReducer?                                        │
│      └── 🟡 OPCIONAL - Para estado global                               │
│                                                                         │
│  [?] useState isolado?                                                  │
│      └── ✅ SIM - Mínimo necessário, máxima simplicidade                │
│                                                                         │
│  DECISÃO: useState para cada seção + useMemo para cálculos              │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                         D3: ESTILIZAÇÃO                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  [?] CSS Modules?                                                       │
│      └── ❌ NÃO - Mais complexidade                                     │
│                                                                         │
│  [?] Tailwind puro?                                                     │
│      └── 🟡 PARCIAL - Para layouts utilitários                          │
│                                                                         │
│  [?] Tailwind + Shadcn UI?                                              │
│      └── ✅ SIM - Componentes prontos + customização                    │
│                                                                         │
│  [?] Manter tema Asgard (navy/gold)?                                    │
│      └── ✅ SIM - Tailwind config custom colors                         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                         D4: INTEGRAÇÕES API                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  [?] Server Actions (Next.js 14+)?                                      │
│      └── ✅ SIM - Para ViaCEP, BrasilAPI (simples, sem cache)           │
│                                                                         │
│  [?] API Routes (app/api/*)?                                            │
│      └── 🟡 OPCIONAL - Para integrações complexas (IBGE cache)           │
│                                                                         │
│  [?] Client-side fetch direto?                                          │
│      └── 🟡 SIM - Para CEP (experiência instantânea)                    │
│                                                                         │
│  [?] Caching (React Query/SWR)?                                         │
│      └── ❌ NÃO - Overkill para este escopo                            │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                         D5: COMPONENTES CUSTOM                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  [?] Sistema de Assinaturas Canvas                                      │
│      └── ✅ CUSTOM - Componente React + HTML5 Canvas                    │
│          (não existe equivalente Shadcn)                                │
│                                                                         │
│  [?] Tabelas CRUD de Produtos/Equipamentos                              │
│      └── 🟡 ADAPTADO - Shadcn Table + custom inline editing              │
│                                                                         │
│  [?] Input Masks (CNPJ, CEP, Telefone)                                  │
│      └── ✅ CUSTOM - Hook useInputMask                                  │
│                                                                         │
│  [?] Timeline de Eventos                                                  │
│      └── 🟡 ADAPTADO - Shadcn components + custom timeline               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 4. ESTRUTURA DE ARQUIVOS SIMPLIFICADA

```
my-app/
├── app/
│   ├── page.tsx                    # Página única - TODA a aplicação
│   ├── layout.tsx                  # Layout com fonts
│   ├── globals.css                 # Tailwind + tema Asgard
│   ├── actions/
│   │   ├── cep.ts                  # Server Action: ViaCEP
│   │   ├── cnpj.ts                 # Server Action: BrasilAPI CNPJ
│   │   └── ibge.ts                 # Server Action: IBGE
│   └── api/
│       └── print/
│           └── route.ts            # API route para geração de PDF
├── components/
│   ├── ui/                         # Shadcn components (npx shadcn add)
│   ├── signature-canvas.tsx        # Componente custom: assinatura
│   ├── product-table.tsx           # Tabela de produtos CRUD
│   ├── equipment-table.tsx         # Tabela de equipamentos CRUD
│   ├── kpi-panel.tsx               # Painel de KPIs
│   ├── timeline.tsx                # Timeline de eventos
│   ├── tag-system.tsx              # Sistema de tags
│   └── shortcut-panel.tsx          # Painel de atalhos
├── hooks/
│   ├── use-input-mask.ts           # Hook para máscaras
│   ├── use-local-storage.ts        # Hook para autosave
│   └── use-timer.ts                # Hook para timer
├── lib/
│   ├── utils.ts                    # cn() e utilitários
│   ├── formatters.ts               # Formatação moeda/data
│   ├── validators.ts               # Validação CNPJ/CPF
│   └── constants.ts                # Produtos mock, tabelas preço
├── types/
│   └── index.ts                    # TypeScript interfaces
├── public/
│   └── (assets estáticos)
├── tailwind.config.ts               # Tema Asgard colors
├── next.config.js
└── package.json
```

---

## 5. MAPA DE COMPONENTES SHADCN NECESSÁRIOS

### 5.1 Instalação dos Componentes

```bash
# Componentes essenciais
npx shadcn add button
npx shadcn add card
npx shadcn add input
npx shadcn add label
npx shadcn add select
npx shadcn add textarea
npx shadcn add badge
npx shadcn add checkbox
npx shadcn add collapsible
npx shadcn add toast          # ou sonner
npx shadcn add sheet
npx shadcn add scroll-area
npx shadcn add separator
npx shadcn add table
npx shadcn add tooltip
npx shadcn add progress
npx shadcn add breadcrumb
npx shadcn add command        # Para autocomplete
npx shadcn add popover        # Para autocomplete
npx shadcn add avatar         # Para timeline
```

### 5.2 Tema Customizado (tailwind.config.ts)

```typescript
const config = {
  theme: {
    extend: {
      colors: {
        navy: {
          DEFAULT: '#1a3a5c',
          light: '#2c5f8a',
          dark: '#0f2438',
        },
        gold: {
          DEFAULT: '#c8a84b',
          light: '#e0be6a',
        },
        cream: '#f8f4ef',
        border: '#b0bec5',
        asgard: {
          success: '#2e7d32',
          warning: '#f57c00',
          error: '#c62828',
          info: '#1565c0',
        }
      },
      fontFamily: {
        barlow: ['Barlow', 'sans-serif'],
        'barlow-condensed': ['Barlow Condensed', 'sans-serif'],
      },
    },
  },
}
```

---

## 6. IMPLEMENTAÇÃO POR SEÇÃO

### 6.1 State Principal (simplificado)

```typescript
// app/page.tsx - State central
interface PedidoState {
  // Dados do Pedido
  id: string;
  data: string;
  vendedor: string;
  observacoes: string;
  segmentoCanal: string;
  segmentoOutros: string;
  canalVenda: string;
  canalConsumo: string;
  tabelaPreco: string;
  tipoEntrega: 'ENTREGA_PROPRIA' | 'RETIRADA_CLIENTE';
  tags: string[];
  
  // Dados do Cliente
  cliente: {
    razao: string;
    fantasia: string;
    cnpj: string;
    ie: string;
    telefone: string;
    celular: string;
    cep: string;
    cidade: string;
    endereco: string;
    pagamento: string;
  };
  
  // Condições
  condicoes: {
    tabelaPreco: string;
    condicaoPagamento: string;
    descontoGlobal: number;
    observacoes: string;
  };
  
  // Produtos e Equipamentos
  produtos: ProdutoItem[];
  equipamentos: EquipamentoItem[];
  
  // Assinaturas
  assinaturas: {
    responsavel: string | null;
    cliente: string | null;
    testemunha: string | null;
  };
  
  // UI State
  timeline: TimelineEvent[];
  tempoDecorrido: number;
  status: 'rascunho' | 'emitido';
}
```

### 6.2 Hooks Custom Necessários

```typescript
// hooks/use-input-mask.ts
export function useInputMask(mask: 'cnpj' | 'cpf' | 'cep' | 'phone' | 'cell') {
  // Implementação das máscaras existentes
}

// hooks/use-local-storage.ts
export function useLocalStorage<T>(key: string, initialValue: T) {
  // Autosave a cada 30s
}

// hooks/use-timer.ts
export function useTimer() {
  // Retorna tempo formatado HH:MM:SS
}
```

### 6.3 Server Actions (App Router)

```typescript
// app/actions/cep.ts
'use server';

export async function buscarEnderecoPorCEP(cep: string) {
  const response = await fetch(`https://viacep.com.br/ws/${cep}/json/`);
  return response.json();
}

// app/actions/cnpj.ts
export async function buscarDadosCNPJ(cnpj: string) {
  const response = await fetch(`https://brasilapi.com.br/api/cnpj/v1/${cnpj}`);
  return response.json();
}

// app/actions/ibge.ts
export async function buscarEstados() {
  const response = await fetch('https://servicodados.ibge.gov.br/api/v1/localidades/estados');
  return response.json();
}
```

---

## 7. FEATURES QUE PRECISAM DE IMPLEMENTAÇÃO CUSTOM

### 7.1 Sistema de Assinaturas (CRITICAL)

```typescript
// components/signature-canvas.tsx
'use client';

import { useRef, useEffect, useState } from 'react';
import { Button } from '@/components/ui/button';
import { Card } from '@/components/ui/card';

interface SignatureCanvasProps {
  label: string;
  onSave: (dataUrl: string) => void;
  width?: number;
  height?: number;
}

export function SignatureCanvas({ 
  label, 
  onSave, 
  width = 300, 
  height = 100 
}: SignatureCanvasProps) {
  const canvasRef = useRef<HTMLCanvasElement>(null);
  const [hasSignature, setHasSignature] = useState(false);
  const [isDrawing, setIsDrawing] = useState(false);
  
  // Implementar: mouse events, touch events, clear, save
  // Conversão direta do código HTML existente para React
  
  return (
    <Card className="p-4">
      <canvas
        ref={canvasRef}
        width={width}
        height={height}
        className="border-2 border-dashed border-border rounded cursor-crosshair touch-none bg-muted/30"
        // ... event handlers
      />
      <div className="text-center mt-2">
        <span className="text-xs font-semibold uppercase text-navy-light">
          {label}
        </span>
      </div>
      <div className="flex gap-2 justify-center mt-2">
        <Button variant="outline" size="sm" onClick={clear}>Limpar</Button>
        <Button size="sm" onClick={save}>Salvar</Button>
      </div>
    </Card>
  );
}
```

### 7.2 Tabela de Produtos Inline Editable

```typescript
// components/product-table.tsx
'use client';

import { useState } from 'react';
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from '@/components/ui/table';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select';
import { Command, CommandEmpty, CommandGroup, CommandInput, CommandItem } from '@/components/ui/command';
import { Popover, PopoverContent, PopoverTrigger } from '@/components/ui/popover';

interface ProdutoItem {
  id: string;
  produto: string;
  tipoEquipamento: string;
  operacao: 'VENDA' | 'CONSIGNADO' | 'TROCA' | 'PERMUTA' | 'BONIFICACAO';
  quantidade: number;
  precoUnitario: number;
  desconto: number;
  valor: number;
}

// Operações com estilos condicionais:
// - BONIFICACAO/PERMUTA: preço zerado, fundo verde/amarelo
// - CONSIGNADO: alerta para data de retorno
```

### 7.3 Sistema de Tags

```typescript
// components/tag-system.tsx
'use client';

import { useState } from 'react';
import { Badge } from '@/components/ui/badge';
import { Input } from '@/components/ui/input';
import { X } from 'lucide-react';

const TAGS_PREDEFINIDAS = [
  { id: 'VIP', label: '⭐ VIP', color: '#c8a84b' },
  { id: 'NOVO_CLIENTE', label: '🆕 Novo Cliente', color: '#1565c0' },
  { id: 'REATIVADO', label: '🔄 Reativado', color: '#2e7d32' },
  { id: 'ALTA_SAZON', label: '📅 Alta Sazonalidade', color: '#f57c00' },
  { id: 'PGTO_PONTUAL', label: '✅ Pgto Pontual', color: '#2e7d32' },
  { id: 'INADIMPLENTE', label: '⚠️ Inadimplente', color: '#c62828' },
  { id: 'EVENTO_ESPEC', label: '🎉 Evento Especial', color: '#7b1fa2' },
  { id: 'FRANQUIA', label: '🏪 Franquia', color: '#0277bd' },
];
```

### 7.4 Impressão (PDF Generation)

Opções:
1. **react-to-print**: Impressão direta mantendo CSS
2. **@react-pdf/renderer**: Geração de PDF programática
3. **jspdf + html2canvas**: Conversão de HTML para PDF

Recomendação: **react-to-print** (menor mudança do código existente)

---

## 8. ATALHOS DE TECLADO (Keyboard Shortcuts)

```typescript
// hooks/use-keyboard-shortcuts.ts
'use client';

import { useEffect } from 'react';

export function useKeyboardShortcuts(handlers: {
  onSearch: () => void;
  onSave: () => void;
  onPrint: () => void;
  onNew: () => void;
  onExport: () => void;
  onImport: () => void;
  onAssistant: () => void;
  onReset: () => void;
}) {
  useEffect(() => {
    const handleKeyDown = (e: KeyboardEvent) => {
      // Ctrl+K: Busca
      if (e.ctrlKey && e.key === 'k') {
        e.preventDefault();
        handlers.onSearch();
      }
      
      // Ctrl+S: Salvar
      if (e.ctrlKey && e.key === 's') {
        e.preventDefault();
        handlers.onSave();
      }
      
      // Ctrl+P: Imprimir
      if (e.ctrlKey && e.key === 'p') {
        e.preventDefault();
        handlers.onPrint();
      }
      
      // Ctrl+N: Novo
      if (e.ctrlKey && e.key === 'n') {
        e.preventDefault();
        handlers.onNew();
      }
      
      // Ctrl+E: Exportar
      if (e.ctrlKey && e.key === 'e') {
        e.preventDefault();
        handlers.onExport();
      }
      
      // Ctrl+I: Importar
      if (e.ctrlKey && e.key === 'i') {
        e.preventDefault();
        handlers.onImport();
      }
      
      // Ctrl+Shift+A: Assistente
      if (e.ctrlKey && e.shiftKey && e.key === 'A') {
        e.preventDefault();
        handlers.onAssistant();
      }
      
      // Ctrl+Shift+R: Reset
      if (e.ctrlKey && e.shiftKey && e.key === 'R') {
        e.preventDefault();
        handlers.onReset();
      }
      
      // F1: Ajuda (Assistente)
      if (e.key === 'F1') {
        e.preventDefault();
        handlers.onAssistant();
      }
    };

    window.addEventListener('keydown', handleKeyDown);
    return () => window.removeEventListener('keydown', handleKeyDown);
  }, [handlers]);
}
```

---

## 9. PRODUTOS MOCK (50+ itens)

```typescript
// lib/constants.ts
export const PRODUTOS_MOCK = [
  { nome: 'Chopp Pilsen 20L', tipo: 'Barril 20L', preco: 180.0, estoque: 50 },
  { nome: 'Chopp Pilsen 30L', tipo: 'Barril 30L', preco: 250.0, estoque: 30 },
  { nome: 'Chopp Pilsen 50L', tipo: 'Barril 50L', preco: 380.0, estoque: 20 },
  { nome: 'Chopp Golden 20L', tipo: 'Barril 20L', preco: 200.0, estoque: 45 },
  { nome: 'Chopp Golden 30L', tipo: 'Barril 30L', preco: 280.0, estoque: 25 },
  { nome: 'Chopp Golden 50L', tipo: 'Barril 50L', preco: 420.0, estoque: 15 },
  { nome: 'Chopp IPA 20L', tipo: 'Barril 20L', preco: 220.0, estoque: 35 },
  // ... continuar lista completa
] as const;

export const TABELAS_PRECO = {
  PADRAO: { multiplicador: 1.0, label: 'Tabela Padrão' },
  ATACADO: { multiplicador: 0.82, label: 'Tabela Atacado' },
  FOOD_SVC: { multiplicador: 0.9, label: 'Food Service' },
  PROMO: { multiplicador: 0.75, label: 'Promoção' },
} as const;

export const EQUIPAMENTOS_MOCK = [
  'Barril 20L Alumínio',
  'Barril 30L Alumínio',
  'Barril 50L Alumínio',
  // ... continuar lista
] as const;
```

---

## 10. CHECKLIST DE MIGRAÇÃO

### Fase 1: Setup (1-2 horas)
- [ ] `npx shadcn@latest init`
- [ ] Configurar tailwind.config.ts com tema Asgard
- [ ] Instalar componentes Shadcn necessários
- [ ] Configurar fonts (Barlow, Barlow Condensed)
- [ ] Criar estrutura de pastas

### Fase 2: Componentes Core (4-6 horas)
- [ ] Header Cockpit
- [ ] KPI Panel
- [ ] Form sections (Dados Pedido, Cliente, Condições)
- [ ] Sidebar (Timeline + Atalhos)

### Fase 3: Lógica de Negócio (6-8 horas)
- [ ] Sistema de Produtos (tabela CRUD)
- [ ] Sistema de Equipamentos (tabela CRUD)
- [ ] Cálculos automáticos (totais, margem)
- [ ] Tabela de preços com multiplicadores
- [ ] Validações (CNPJ, CPF, CEP)

### Fase 4: Features Avançadas (4-6 horas)
- [ ] Sistema de Assinaturas (Canvas)
- [ ] Sistema de Tags
- [ ] Autocomplete de produtos
- [ ] Drawer Assistente
- [ ] Toast notifications

### Fase 5: Integrações (2-4 horas)
- [ ] Server Actions para APIs externas
- [ ] Integração ViaCEP
- [ ] Integração BrasilAPI
- [ ] Integração IBGE

### Fase 6: Utilities (2-3 horas)
- [ ] Atalhos de teclado
- [ ] Autosave localStorage
- [ ] Exportação JSON
- [ ] Importação CSV
- [ ] Sistema de impressão

### Fase 7: Polimento (2-3 horas)
- [ ] Responsividade
- [ ] Animações/transições
- [ ] Testes manuais
- [ ] Ajustes de acessibilidade

---

## 11. ESTIMATIVA DE TEMPO

| Fase | Tempo Estimado |
|------|----------------|
| Setup | 1-2h |
| Componentes Core | 4-6h |
| Lógica de Negócio | 6-8h |
| Features Avançadas | 4-6h |
| Integrações | 2-4h |
| Utilities | 2-3h |
| Polimento | 2-3h |
| **TOTAL** | **21-32 horas** |

---

## 12. RISCOS E MITIGAÇÕES

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|-----------|-----------|
| Canvas de assinaturas complexo | Média | Alto | Isolar em componente dedicado, testar touch events |
| Tabela CRUD inline complexa | Média | Médio | Usar Shadcn Table como base, customizar células |
| Autocomplete com grandes listas | Baixa | Médio | Virtualização ou debounce no Command |
| Performance com muitos produtos | Baixa | Médio | Paginação ou virtualização na tabela |
| Impressão A4 com CSS complexo | Média | Alto | Usar react-to-print, manter CSS existente |

---

## 13. CONCLUSÃO

### Possibilidade: ✅ **100% VIÁVEL**

O sistema pode ser completamente migrado para Next.js + Shadcn UI mantendo:
- ✅ Todas as 50+ features existentes
- ✅ Tema visual Asgard (navy/gold)
- ✅ Complexidade de negócio (tabelas de preço, operações)
- ✅ Integrações com APIs brasileiras
- ✅ UX avançada (atalhos, timeline, tags)

### Próximos Passos Recomendados:

1. **Iniciar projeto**: `npx shadcn@latest init`
2. **Migrar por seções**: Começar pelo Header → KPIs → Form Wizard
3. **Testar integrações**: Validar APIs ViaCEP, BrasilAPI
4. **Validar assinaturas**: Testar em desktop e mobile
5. **Teste final de impressão**: Garantir layout A4 correto

---

**Documento gerado após análise completa de `pedidosv1-3.html` (5.813 linhas)**
