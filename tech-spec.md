# Техническое задание: Сайт Патентного Бюро

## Архитектура проекта

```
app/
├── sections/
│   ├── Header.tsx          # Навигация с glassmorphism
│   ├── Hero.tsx            # Hero с 3D-элементами
│   ├── Clients.tsx         # Логотипы клиентов (infinite scroll)
│   ├── Services.tsx        # Карточки услуг
│   ├── FreeServices.tsx    # Бесплатные сервисы
│   ├── MediaPulse.tsx      # Медиа-пульс
│   ├── Team.tsx            # Команда экспертов
│   ├── Stats.tsx           # Статистика с счетчиками
│   ├── Testimonials.tsx    # Отзывы клиентов
│   ├── FAQ.tsx             # Часто задаваемые вопросы
│   ├── CTA.tsx             # Призыв к действию
│   └── Footer.tsx          # Подвал
├── components/
│   ├── ui/                 # shadcn/ui компоненты
│   ├── AnimatedCounter.tsx # Анимированный счетчик
│   ├── ServiceCard.tsx     # Карточка услуги
│   ├── ExpertCard.tsx      # Карточка эксперта
│   ├── TestimonialCard.tsx # Карточка отзыва
│   ├── FAQItem.tsx         # Элемент аккордеона
│   └── LogoScroller.tsx    # Бесконечная прокрутка логотипов
├── hooks/
│   ├── useScrollAnimation.ts
│   ├── useMousePosition.ts
│   └── useInView.ts
├── lib/
│   └── utils.ts
├── page.tsx
├── layout.tsx
└── globals.css
```

## Компоненты и их реализация

### 1. Header
**Функционал:**
- Фиксированная позиция при скролле
- Glassmorphism эффект (backdrop-filter: blur)
- Выпадающие меню для СЕРВИСЫ, УСЛУГИ, ДЛЯ КЛИЕНТОВ
- Адаптивное меню (hamburger на мобильных)

**Анимации:**
- Scroll-triggered background change
- Dropdown animation с translateY и opacity
- Hover underline animation

**Зависимости:**
- @radix-ui/react-dropdown-menu
- framer-motion (для анимаций)

### 2. Hero
**Функционал:**
- Двухколоночный layout
- 3D-элементы с parallax эффектом
- Поисковая форма

**Анимации:**
- Text reveal с stagger (GSAP или Framer Motion)
- 3D cards floating animation (CSS keyframes)
- Mouse parallax (custom hook)

**Зависимости:**
- framer-motion
- three.js (опционально для 3D)

### 3. Clients (Logo Scroller)
**Функционал:**
- Бесконечная горизонтальная прокрутка
- Дублирование контента для seamless loop

**Анимации:**
- CSS animation translateX
- Pause on hover

**Реализация:**
- Чистый CSS animation
- Дублирование списка логотипов

### 4. Services
**Функционал:**
- Сетка карточек 3x2
- Hover effects на карточках

**Анимации:**
- Scroll-triggered entrance (stagger)
- Card lift on hover
- Image scale on hover
- Shadow animation

**Зависимости:**
- framer-motion (ScrollTrigger)

### 5. FreeServices
**Функционал:**
- Три карточки с формами
- Поисковые поля
- Кнопка калькулятора

**Анимации:**
- Different entrance directions
- Input focus glow effect
- Button hover animation

### 6. MediaPulse
**Функционал:**
- Masonry-like grid
- Карточки разных размеров

**Анимации:**
- Staggered reveal
- Hover overlay
- Arrow animation

### 7. Team
**Функционал:**
- Горизонтальный скролл
- Карточки экспертов

**Анимации:**
- Horizontal scroll on vertical scroll
- Card hover effects

### 8. Stats
**Функционал:**
- Анимированные счетчики
- Сетка 4x1

**Анимации:**
- Counter animation (0 to value)
- Staggered appearance

**Реализация:**
- Custom AnimatedCounter component
- Intersection Observer для запуска

### 9. Testimonials
**Функционал:**
- Карусель отзывов
- Автопрокрутка
- Навигация

**Анимации:**
- Slide transitions
- Pause on hover

**Зависимости:**
- embla-carousel-react

### 10. FAQ
**Функционал:**
- Аккордеон
- Открытие/закрытие вопросов

**Анимации:**
- Height animation
- Icon rotation

**Зависимости:**
- @radix-ui/react-accordion

### 11. CTA
**Функционал:**
- Кнопка CTA
- Социальные иконки

**Анимации:**
- Button pulse
- Social icons bounce

### 12. Footer
**Функционал:**
- 4-колоночный layout
- Ссылки
- Контактная информация

**Анимации:**
- Link hover underline
- Fade in on scroll

## Хуки

### useScrollAnimation
```typescript
// Отслеживание скролла для анимаций
// Возвращает scrollY, scrollDirection, isScrolled
```

### useMousePosition
```typescript
// Отслеживание позиции мыши для parallax
// Возвращает x, y относительно окна
```

### useInView
```typescript
// Intersection Observer wrapper
// Запуск анимаций когда элемент в viewport
```

## Утилиты

### AnimatedCounter
```typescript
interface AnimatedCounterProps {
  end: number;
  duration?: number;
  suffix?: string;
  prefix?: string;
}
```

### Animation Variants (Framer Motion)
```typescript
// Fade up
const fadeUp = {
  hidden: { opacity: 0, y: 40 },
  visible: { opacity: 1, y: 0 }
};

// Stagger container
const staggerContainer = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: { staggerChildren: 0.15 }
  }
};

// Scale on hover
const scaleOnHover = {
  rest: { scale: 1 },
  hover: { scale: 1.05 }
};
```

## CSS Animations

### Floating Animation
```css
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-20px); }
}
```

### Infinite Scroll
```css
@keyframes scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
```

### Pulse
```css
@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(200, 255, 46, 0.4); }
  50% { box-shadow: 0 0 0 20px rgba(200, 255, 46, 0); }
}
```

## Зависимости проекта

### Core
- next
- react
- react-dom
- typescript

### UI
- @radix-ui/react-dropdown-menu
- @radix-ui/react-accordion
- @shadcn/ui components
- lucide-react

### Animation
- framer-motion
- gsap (опционально)

### Carousel
- embla-carousel-react

### Styling
- tailwindcss
- tailwind-merge
- clsx

## Performance Optimizations

1. **will-change** на анимируемых элементах
2. **transform3d** для GPU acceleration
3. **Lazy loading** изображений
4. **Code splitting** по секциям
5. **Reduced motion** support

## Адаптивность

### Breakpoints
```css
/* Tailwind */
sm: 640px
md: 768px
lg: 1024px
xl: 1280px
2xl: 1536px
```

### Mobile-first подход
- Базовые стили для mobile
- Медиа-запросы для больших экранов
