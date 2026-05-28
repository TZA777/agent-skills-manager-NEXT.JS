step1: create next.js app
step2: crate basic pages 
    (auth)---->login, register
    about

step3:  login & register pages
        we have forms and onSubmit----> useAuth() ---> login in register logic is handled
        layout.tsx----> login form and register form are centered

step4: hooks/useAuth.tsx
        login, register, logout logics are handled
        AuthContext is created and provided for global use 

        in tsconfig.json--->@ to address folders inside app
        "paths": {
      "@/*": ["./app/*"]
    }

step5: basic about page

step6: addressing api
        auth API's
        skills API's

        auth API's--->
        login/route.ts---> POST req handling login request
        logout/route.ts
        register/route.ts
        me/route.ts


step7: prisma ORM and postgres setup
        1. installations
        2. schema file
        3. lib/prisma.ts
        4. DATABASE URL in dotenv


step8: lib/auth.ts
        handles
        hashPassword
        verifyPassword
        generateToken
        verifyToken
        setAuthCookie
        clearAuthCookie
        getAuthToken
        getCurrentUser
        extractTokenFromRequest

step9: api for skills
        api/skills/route.ts-----------> handling skills 
        api/skills/[id]/route.ts------> handling individual skills


step10: actions/skills.ts
        server actions handling 
        createSkill
        updateSkill
        deleteSkill

step11: componests/Header.tsx, Footer.tsx, Providers.tsx
        Header.tsx---> hadling navbar
        Footer.tsx---> handling footer
        Provider.tsx---> hadling AuthProvider

step12: update pages----> dashboard for user and skills for public 

step13: update global pages and global page.tsx

step14: moving to cloud db NEON: 
        1. in neon create account
        2. update db url in env
        3. a or b

            a: npx prisma db push
            b: (Migration-Based)------->npx prisma migrate dev --name init  +  npm run dev

            next Verify Connection
            npx prisma db pull
            npx prisma generate

        4. npm run dev and try to add skills and check neon DB

===============================================================================
FOR DEPLOYMENT follow deploymentGuide.md



