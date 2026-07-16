# Week1 核心产出汇总 & Mini Demo 0 提交文档
仓库链接：https://github.com/bb-cmb/-/tree/9609ddedd3d0777e47fecf6ab52ec622e4972b99/build_logs1

## 一、Mini Demo 0 完整说明（极简链上留言板合约Demo）
### 1. 整体完成内容
搭建完整极简留言板链上闭环Demo：使用AI生成Solidity合约初稿，人工审计校验后部署至Monad Testnet，完成链上读写交互，将钱包配置、合约编译、部署、交互、区块浏览器核验全流程图文归档至仓库`build_logs1`目录。

### 2. 真实链上操作内容
1. 新建独立MetaMask课程钱包，配置Monad Testnet，领取测试MON完成钱包自转账；
2. 在Remix编译`MessageBoard`留言板合约并部署上链；
3. 执行`write`写入留言、`message`读取留言两次链上合约交互；
4. 在MonadVision区块浏览器核验钱包、合约、全部交易数据。
- 课程钱包地址：`0xD1A61BA21437533401F300FCC122EF263E93dEa8`
- 留言板合约地址：`0xE10B2F8c6352345e851d89e1fCD1Be4796A8E607`
(1.内容具体查看Web3-Day1.md内容;2.3.4.具体查看Web3-Day2.md内容)

### 3. AI辅助完成内容
1. 根据自定义Prompt生成可直接编译运行的留言板Solidity合约代码；
2. 自动拆解合约结构，解释状态变量、构造函数、读写函数逻辑；
3. 协助生成Markdown笔记、学习总结初稿并规范排版。
(1.2.具体查看Web3-Day2.md内容)

### 4. 人工判断与修改工作
1. 合约安全审计：校验开源许可证、编译器版本、Gas优化、访问权限，补充标准化NatSpec注释；
2. 链上数据核验：手动打开区块浏览器核对每笔交易状态、Gas消耗、合约存储内容；
3. 赛道价值判断：结合Monad底层特性人工筛选适配的高频交互赛道，完成产品适配分析；
4. 建立人机协作规范：识别AI代码安全隐患，制定多层人工审查标准。
(具体查看Web3-Day2.md内容)

### 5. 后续持续推进方向
选择**Research**赛道，围绕Monad生态赛道、用户需求、底层技术差异持续输出行业分析、竞品复盘、产品可行性研究文档。

## 二、提交材料清单
1. Week1作品仓库链接：https://github.com/bb-cmb/-/tree/9609ddedd3d0777e47fecf6ab52ec622e4972b99/build_logs1
2. Demo配套材料：仓库内完整学习README文档 + 全流程截图（钱包配置、合约编译、部署交互、区块浏览器校验、AI代码审计记录）(具体查看Web3-Day2.md，README.md和1README.md内容)
3. Week2主方向选择：Research
4. 作品集/简历一句话描述
独立完成Monad测试网完整链上Demo，熟练掌握AI辅助智能合约开发与人机协同安全审计流程，熟悉Monad与以太坊底层差异化特性，具备Web3赛道调研、生态产品分析与落地研判能力。
5. Week2计划持续推进的问题
1. 如何撰写标准化、专业的Monad生态赛道研究报告，是否有行业范文可供参考；
2. 如何区分“技术可行”与“用户真实需求”，精准判断高频链上产品落地价值；
3. 调研Monad异步执行、储备余额机制对产品设计的隐藏约束，搜集相关落地实操案例。

## 基于Message最小Solidity合约生成DApp(大部分AI生成)

已生成 `index.html`，以下是功能对照和 `index.html`代码内容：

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <!--
    ╔══════════════════════════════════════════════════════════════╗
    ║           MessageBoard DApp — Remix 部署指南                 ║
    ╠══════════════════════════════════════════════════════════════╣
    ║                                                            ║
    ║  📌 如何在 Remix 部署合约并获取 ABI：                       ║
    ║  1. 打开 https://remix.ethereum.org                        ║
    ║  2. 新建 MessageBoard.sol，粘贴以下合约代码：               ║
    ║     // SPDX-License-Identifier: MIT                        ║
    ║     pragma solidity ^0.8.20;                               ║
    ║     contract MessageBoard {                                ║
    ║         string public message;                             ║
    ║         function write(string calldata m) external {       ║
    ║             message = m;                                   ║
    ║         }                                                  ║
    ║     }                                                      ║
    ║  3. 点击左侧 "Solidity Compiler" → Compile                 ║
    ║  4. 点击左侧 "Deploy & Run"                                ║
    ║     Environment 选 "Injected Provider - MetaMask"          ║
    ║  5. MetaMask 切换至 Monad Testnet 测试网，点击 Deploy      ║
    ║  6. 部署完成后，复制合约地址填入本页 CONTRACT_ADDRESS       ║
    ║                                                            ║
    ║  📌 如何获取 ABI（如果需要）：                             ║
    ║  在 Solidity Compiler 选项卡底部，点击 ABI 旁的复制按钮    ║
    ║  即可获得完整 ABI JSON。本页面已内置 ABI，无需手动复制。   ║
    ║                                                            ║
    ║  📌 获取 Monad 测试网代币（水龙头）：                      ║
    ║  https://testnet.monad.xyz                                 ║
    ║                                                            ║
    ╚══════════════════════════════════════════════════════════════╝
    -->
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>MessageBoard — 极简链上留言板</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet" />
    <script src="https://cdn.jsdelivr.net/npm/ethers@6.13.4/dist/ethers.umd.min.js"></script>

    <style>
        :root {
            --bg-1: #0c0c1d;
            --bg-2: #12122a;
            --glass: rgba(255,255,255,0.04);
            --glass-border: rgba(255,255,255,0.07);
            --glass-hover: rgba(255,255,255,0.08);
            --purple: #8b5cf6;
            --purple-light: #a78bfa;
            --pink: #ec4899;
            --text: #e2e8f0;
            --text-2: #94a3b8;
            --text-3: #64748b;
            --green: #34d399;
            --red: #f87171;
            --amber: #fbbf24;
            --radius: 18px;
            --radius-sm: 12px;
        }
        *{margin:0;padding:0;box-sizing:border-box}
        body{
            font-family:'Inter',-apple-system,BlinkMacSystemFont,sans-serif;
            min-height:100vh;
            background:linear-gradient(150deg,var(--bg-1) 0%,var(--bg-2) 50%,#1a1040 100%);
            color:var(--text);
            display:flex;align-items:flex-start;justify-content:center;
            padding:32px 16px 80px;
            position:relative;overflow-x:hidden;line-height:1.6;
        }
        /* 背景光晕 */
        body::before,body::after{
            content:'';position:fixed;border-radius:50%;pointer-events:none;z-index:0;filter:blur(130px);opacity:.35;
        }
        body::before{top:-15%;left:-10%;width:550px;height:550px;background:radial-gradient(circle,rgba(139,92,246,.3) 0%,transparent 70%)}
        body::after{bottom:-10%;right:-8%;width:450px;height:450px;background:radial-gradient(circle,rgba(236,72,153,.25) 0%,transparent 70%)}

        #app{position:relative;z-index:1;width:100%;max-width:640px;display:flex;flex-direction:column;gap:16px}

        /* ── 玻璃卡片 ── */
        .card{
            background:var(--glass);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);
            border:1px solid var(--glass-border);border-radius:var(--radius);padding:26px 28px;
            transition:border-color .25s,background .25s;
        }
        .card-accent{border-color:rgba(139,92,246,.18);background:rgba(139,92,246,.035)}

        /* ── 品牌 ── */
        .brand{display:flex;align-items:center;gap:12px}
        .brand .icon{font-size:2rem}
        .brand h1{font-size:1.7rem;font-weight:800;background:linear-gradient(135deg,var(--purple-light),var(--pink));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;letter-spacing:-.5px}
        .brand .sub{font-size:.82rem;color:var(--text-2);font-weight:400;margin-top:2px}

        /* ── 可折叠指南 ── */
        .guide-toggle{
            display:flex;align-items:center;justify-content:space-between;cursor:pointer;user-select:none;
            padding:14px 28px;border-radius:var(--radius) var(--radius) 0 0;
        }
        .guide-toggle:hover{background:rgba(255,255,255,.03)}
        .guide-toggle h3{font-size:.92rem;font-weight:600;color:var(--purple-light);display:flex;align-items:center;gap:8px}
        .guide-toggle .arr{transition:transform .3s;font-size:.75rem;color:var(--text-3)}
        .guide-toggle .arr.open{transform:rotate(180deg)}
        .guide-body{max-height:0;overflow:hidden;transition:max-height .4s ease;padding:0 28px}
        .guide-body.open{max-height:500px;padding:0 28px 18px}
        .step{display:flex;gap:10px;margin-bottom:10px;font-size:.82rem;color:var(--text-2);line-height:1.65}
        .step-num{flex-shrink:0;width:22px;height:22px;border-radius:50%;background:rgba(139,92,246,.15);color:var(--purple-light);font-size:.72rem;font-weight:700;display:flex;align-items:center;justify-content:center}
        .step code{font-size:.76rem;background:rgba(0,0,0,.35);padding:1px 7px;border-radius:5px;color:var(--green);font-family:Consolas,monospace;word-break:break-all}
        .step a{color:var(--purple-light);text-decoration:underline;text-underline-offset:3px}

        /* ── 顶部栏 ── */
        .top-bar{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px}
        .chip{
            display:inline-flex;align-items:center;gap:6px;padding:6px 14px;border-radius:20px;
            font-size:.78rem;font-weight:600;
        }
        .chip-ok{background:rgba(52,211,153,.12);color:var(--green);border:1px solid rgba(52,211,153,.25)}
        .chip-warn{background:rgba(248,113,113,.12);color:var(--red);border:1px solid rgba(248,113,113,.25)}
        .chip .d{width:7px;height:7px;border-radius:50%}
        .chip-ok .d{background:var(--green)}
        .chip-warn .d{background:var(--red)}
        .addr-tag{
            padding:6px 12px;border-radius:20px;font-size:.8rem;font-weight:500;
            background:rgba(255,255,255,.05);color:var(--text-2);border:1px solid rgba(255,255,255,.08);
            font-family:Consolas,monospace;display:none;
        }

        /* ── 按钮 ── */
        .btn{display:inline-flex;align-items:center;gap:7px;padding:10px 20px;border-radius:var(--radius-sm);font-family:Inter,sans-serif;font-size:.88rem;font-weight:600;border:none;cursor:pointer;transition:all .2s;white-space:nowrap}
        .btn-primary{background:linear-gradient(135deg,var(--purple),#7c3aed);color:#fff;box-shadow:0 4px 16px rgba(139,92,246,.3)}
        .btn-primary:hover:not(:disabled){transform:translateY(-2px);box-shadow:0 8px 28px rgba(139,92,246,.4)}
        .btn-primary:active:not(:disabled){transform:scale(.97)}
        .btn-primary:disabled{opacity:.4;cursor:not-allowed;transform:none;box-shadow:none}
        .btn-outline{background:transparent;color:var(--purple-light);border:1px solid rgba(139,92,246,.35)}
        .btn-outline:hover{background:rgba(139,92,246,.1)}
        .btn-sm{padding:7px 14px;font-size:.8rem;border-radius:8px}
        .btn-ghost{background:rgba(255,255,255,.04);color:var(--text-2);border:1px solid rgba(255,255,255,.07)}
        .btn-ghost:hover{background:rgba(255,255,255,.08);color:var(--text)}

        /* ── 当前留言 ── */
        .msg-display{text-align:center}
        .msg-display .label{font-size:.7rem;text-transform:uppercase;letter-spacing:2.5px;color:var(--text-3);margin-bottom:8px}
        .msg-display .content{font-size:1.4rem;font-weight:600;color:#f1f5f9;word-break:break-word;min-height:48px;display:flex;align-items:center;justify-content:center;padding:6px 0;transition:color .3s}
        .msg-display .content.empty{color:#475569;font-style:italic;font-weight:400;font-size:1.1rem}
        .msg-display .meta{margin-top:10px;font-size:.78rem;color:var(--text-3);display:flex;align-items:center;justify-content:center;gap:14px;flex-wrap:wrap}

        /* ── 输入区 ── */
        .input-row{display:flex;gap:10px}
        .input-row input{flex:1;padding:13px 18px;border-radius:var(--radius-sm);background:rgba(0,0,0,.3);border:1px solid rgba(255,255,255,.07);color:var(--text);font-family:Inter,sans-serif;font-size:.94rem;outline:none;transition:border-color .25s,box-shadow .25s}
        .input-row input::placeholder{color:#52525b}
        .input-row input:focus{border-color:rgba(139,92,246,.45);box-shadow:0 0 0 3px rgba(139,92,246,.1)}
        .char-hint{text-align:right;font-size:.72rem;color:var(--text-3);margin-top:5px}
        .char-hint.warn{color:var(--amber)}

        /* ── Toast ── */
        #toasts{position:fixed;top:24px;right:24px;z-index:9999;display:flex;flex-direction:column;gap:8px;max-width:360px}
        .toast{padding:13px 20px;border-radius:12px;font-size:.86rem;font-weight:500;backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);box-shadow:0 8px 28px rgba(0,0,0,.35);display:flex;align-items:center;gap:10px;animation:toastIn .3s ease}
        .toast.out{animation:toastOut .25s ease forwards}
        .toast-pending{background:rgba(251,191,36,.14);border:1px solid rgba(251,191,36,.3);color:#fde68a}
        .toast-success{background:rgba(52,211,153,.14);border:1px solid rgba(52,211,153,.3);color:#6ee7b7}
        .toast-error{background:rgba(248,113,113,.14);border:1px solid rgba(248,113,113,.3);color:#fca5a5}
        .toast-info{background:rgba(139,92,246,.14);border:1px solid rgba(139,92,246,.3);color:#c4b5fd}
        .toast .spin{display:inline-block;width:15px;height:15px;border:2px solid rgba(251,191,36,.3);border-top-color:var(--amber);border-radius:50%;animation:spin .7s linear infinite;flex-shrink:0}
        @keyframes toastIn{from{opacity:0;transform:translateX(40px)}to{opacity:1;transform:translateX(0)}}
        @keyframes toastOut{from{opacity:1;transform:translateX(0)}to{opacity:0;transform:translateX(40px)}}
        @keyframes spin{to{transform:rotate(360deg)}}

        /* ── 合约地址行 ── */
        .addr-row{display:none;align-items:center;gap:6px;margin-top:8px;font-size:.76rem;color:var(--text-3);flex-wrap:wrap}
        .addr-row code{background:rgba(0,0,0,.35);padding:3px 8px;border-radius:5px;color:var(--green);font-family:Consolas,monospace;font-size:.74rem;word-break:break-all}

        /* ── 底部 ── */
        .footer{text-align:center;font-size:.74rem;color:#3b3b5c;padding-top:6px}

        @media(max-width:500px){
            .input-row{flex-direction:column}
            .top-bar{flex-direction:column;align-items:flex-start}
            .card{padding:20px 16px}
            .brand h1{font-size:1.35rem}
            #toasts{right:8px;left:8px;max-width:none}
        }
    </style>
</head>
<body>

    <div id="toasts"></div>
    <div id="app">
        <!-- 品牌 -->
        <div class="brand">
            <span class="icon">💬</span>
            <div><h1>MessageBoard</h1><p class="sub">极简链上留言板 · Monad Testnet</p></div>
        </div>

        <!-- 部署指南（可折叠） -->
        <div class="card" style="padding:0;overflow:hidden">
            <div class="guide-toggle" onclick="toggleGuide()">
                <h3>📖 如何部署合约</h3><span class="arr open" id="guideArrow">▼</span>
            </div>
            <div class="guide-body open" id="guideBody">
                <div class="step"><span class="step-num">1</span><span>打开 <a href="https://remix.ethereum.org" target="_blank">remix.ethereum.org</a>，新建 <code>MessageBoard.sol</code>，粘贴合约代码并编译。</span></div>
                <div class="step"><span class="step-num">2</span><span>左侧 <strong>Deploy &amp; Run</strong> → Environment 选 <strong>Injected Provider - MetaMask</strong>。</span></div>
                <div class="step"><span class="step-num">3</span><span>MetaMask 切换 <strong>Monad Testnet 测试网</strong>，点击 <strong>Deploy</strong>，确认交易。</span></div>
                <div class="step"><span class="step-num">4</span><span>复制部署后的合约地址（如 <code>0x1234...abcd</code>），填入本页 <code>CONTRACT_ADDRESS</code>。</span></div>
                <div class="step"><span class="step-num">5</span><span>刷新页面，连接钱包，即可读写留言。</span></div>
            </div>
        </div>

        <!-- 钱包连接 -->
        <div class="card top-bar">
            <div>
                <span id="netChip" class="chip chip-warn"><span class="d"></span><span id="netLabel">未连接</span></span>
                <span class="addr-tag" id="addrTag"></span>
            </div>
            <button class="btn btn-primary" id="connectBtn" onclick="connectWallet()">🔗 连接 MetaMask</button>
        </div>

        <!-- 当前留言 -->
        <div class="card card-accent msg-display">
            <div class="label">⛓ 链上当前留言</div>
            <div class="content empty" id="msgContent">— 暂无留言 —</div>
            <div class="meta">
                <span id="msgMeta" style="display:none"></span>
                <button class="btn btn-ghost btn-sm" id="refreshBtn" onclick="refreshMessage()" disabled>🔄 刷新</button>
            </div>
        </div>

        <!-- 写入区 -->
        <div class="card">
            <div class="input-row">
                <input type="text" id="msgInput" placeholder="写下留言..." maxlength="200" autocomplete="off" onkeydown="if(event.key==='Enter')publish()" oninput="updateCount()"/>
                <button class="btn btn-primary" id="publishBtn" onclick="publish()" disabled>✉️ 发布</button>
            </div>
            <div class="char-hint" id="charHint">0 / 200</div>
        </div>

        <!-- 合约地址 -->
        <div class="addr-row" id="addrRow"><span>📄 合约:</span><code id="addrCode"></code></div>
        <div class="footer">MessageBoard DApp · ethers.js v6 · Monad Testnet</div>
    </div>

    <script>
        // ═══════════════════════════════════════════════
        //  🔧 在这里粘贴合约地址
        // ═══════════════════════════════════════════════
        const CONTRACT_ADDRESS = "0xE10B2F8c6352345e851d89e1fCD1Be4796A8E607";(把这里的合约地址改成自己的保存后再打开网站连接MataMask钱包后使用)
        // ═══════════════════════════════════════════════

        const ABI = [
            { inputs: [{ internalType: "string", name: "_newMessage", type: "string" }], name: "write", outputs: [], stateMutability: "nonpayable", type: "function" },
            { inputs: [], name: "message", outputs: [{ internalType: "string", name: "", type: "string" }], stateMutability: "view", type: "function" }
        ];
        const MONAD_TESTNET_ID = 10143;

        let provider = null, signer = null, contract = null, account = null, chainId = null;

        // DOM
        const $ = (id) => document.getElementById(id);
        const connectBtn = $("connectBtn"), publishBtn = $("publishBtn"), refreshBtn = $("refreshBtn");
        const netChip = $("netChip"), netLabel = $("netLabel"), addrTag = $("addrTag");
        const msgContent = $("msgContent"), msgMeta = $("msgMeta"), msgInput = $("msgInput");
        const charHint = $("charHint"), addrRow = $("addrRow"), addrCode = $("addrCode");
        const toasts = $("toasts");

        // ── Toast ──
        function toast(msg, type, ms = 3500) {
            const el = document.createElement("div");
            el.className = `toast toast-${type}`;
            const icons = { pending: '<span class="spin"></span>', success: '✅', error: '❌', info: 'ℹ️' };
            el.innerHTML = `${icons[type] || icons.info}<span>${msg}</span>`;
            toasts.appendChild(el);
            setTimeout(() => { el.classList.add("out"); setTimeout(() => el.remove(), 250); }, ms);
            return el; // pending 时可手动移除
        }

        // ── 格式化 ──
        const short = (a) => a ? a.slice(0, 6) + "..." + a.slice(-4) : "";
        const nowStr = () => { const d = new Date(); return [d.getHours(), d.getMinutes(), d.getSeconds()].map(n => String(n).padStart(2, "0")).join(":"); };

        // ── 字数 ──
        function updateCount() {
            const n = msgInput.value.length;
            charHint.textContent = `${n} / 200`;
            charHint.className = `char-hint${n > 180 ? " warn" : ""}`;
        }

        // ── 折叠 ──
        function toggleGuide() {
            const b = $("guideBody"), a = $("guideArrow"), o = b.classList.contains("open");
            b.classList.toggle("open", !o); a.classList.toggle("open", !o);
        }

        // ═══════════════════════════════════════════════
        //  连接钱包
        // ═══════════════════════════════════════════════
        async function connectWallet() {
            if (!window.ethereum) return toast("请安装 MetaMask 浏览器扩展", "error");
            try {
                const accts = await window.ethereum.request({ method: "eth_requestAccounts" });
                if (!accts.length) return toast("未获取到账户", "error");
                await setup(accts);
                if (chainId !== MONAD_TESTNET_ID) { toast("请切换到 Monad Testnet 测试网", "info", 5000); await switchMonadTestnet(); }
                toast(`已连接: ${short(account)}`, "success");
                if (CONTRACT_ADDRESS) { initContract(); await refreshMessage(); }
            } catch (e) {
                if (e.code === 4001) toast("用户拒绝了连接", "error");
                else toast("连接失败: " + (e.message || e), "error");
            }
        }

        async function setup(accts) {
            provider = new ethers.BrowserProvider(window.ethereum);
            signer = await provider.getSigner();
            account = accts[0];
            const net = await provider.getNetwork();
            chainId = Number(net.chainId);
            updateTopBar();
        }

        function updateTopBar() {
            const ok = chainId === MONAD_TESTNET_ID;
            const names = { 1: "Mainnet", 5: "Goerli", 10143: "Monad Testnet", 11155111: "Sepolia", 137: "Polygon", 80001: "Mumbai", 31337: "Localhost" };
            netLabel.textContent = ok ? "Monad Testnet 测试网" : `${names[chainId] || "Chain " + chainId}`;
            netChip.className = `chip ${ok ? "chip-ok" : "chip-warn"}`;
            connectBtn.textContent = `👤 ${short(account)}`;
            connectBtn.className = "btn btn-outline";
            addrTag.textContent = short(account);
            addrTag.style.display = "inline-flex";
            refreshBtn.disabled = false;
        }

        async function switchMonadTestnet() {
            try {
                await window.ethereum.request({ method: "wallet_switchEthereumChain", params: [{ chainId: "0x" + MONAD_TESTNET_ID.toString(16) }] });
            } catch (e) {
                if (e.code === 4902) {
                    await window.ethereum.request({ method: "wallet_addEthereumChain", params: [{ chainId: "0x" + MONAD_TESTNET_ID.toString(16), chainName: "Monad Testnet", nativeCurrency: { name: "MON", symbol: "MON", decimals: 18 }, rpcUrls: ["https://testnet-rpc.monad.xyz"], blockExplorerUrls: ["https://testnet.monadexplorer.com"] }] });
                }
            }
        }

        function initContract() {
            try {
                contract = new ethers.Contract(CONTRACT_ADDRESS, ABI, signer);
                publishBtn.disabled = false;
                addrCode.textContent = CONTRACT_ADDRESS;
                addrRow.style.display = "flex";
            } catch (e) { toast("合约地址无效", "error"); }
        }

        // ═══════════════════════════════════════════════
        //  读取留言
        // ═══════════════════════════════════════════════
        async function refreshMessage() {
            if (!contract) return;
            refreshBtn.disabled = true; refreshBtn.textContent = "⏳...";
            try {
                const msg = await contract.message();
                if (msg && msg.length > 0) { msgContent.textContent = msg; msgContent.className = "content"; }
                else { msgContent.textContent = "— 暂无留言 —"; msgContent.className = "content empty"; }
                msgMeta.textContent = `取自链上 · ${nowStr()}`;
                msgMeta.style.display = "inline";
            } catch (e) { msgContent.textContent = "读取失败"; msgContent.className = "content empty"; }
            finally { refreshBtn.disabled = false; refreshBtn.textContent = "🔄 刷新"; }
        }

        // ═══════════════════════════════════════════════
        //  写入留言
        // ═══════════════════════════════════════════════
        async function publish() {
            if (!contract) return toast("请先连接钱包并填入合约地址", "error");
            const text = msgInput.value.trim();
            if (!text) return msgInput.focus();

            publishBtn.disabled = true; publishBtn.textContent = "⏳ 确认中...";
            const pendingToast = toast("交易已发送，等待链上确认…", "pending", 99999);

            try {
                const tx = await contract.write(text);
                const receipt = await tx.wait();
                // 移除 pending，显示成功
                pendingToast.classList.add("out");
                setTimeout(() => pendingToast.remove(), 250);
                toast(`✅ 留言已上链！区块: ${receipt.blockNumber}`, "success");
                msgInput.value = "";
                updateCount();
                await refreshMessage();
            } catch (e) {
                pendingToast.classList.add("out");
                setTimeout(() => pendingToast.remove(), 250);
                if (e.code === "ACTION_REJECTED" || e.code === 4001) toast("用户取消了交易", "info");
                else toast("交易失败: " + (e.reason || e.shortMessage || e.message), "error");
            } finally {
                publishBtn.disabled = false; publishBtn.textContent = "✉️ 发布"; msgInput.focus();
            }
        }

        // ═══════════════════════════════════════════════
        //  账户 & 链变化监听
        // ═══════════════════════════════════════════════
        if (window.ethereum) {
            window.ethereum.on("accountsChanged", async (accts) => {
                if (!accts.length) return resetUI();
                await setup(accts);
                toast(`已切换至 ${short(account)}`, "info");
                if (contract) await refreshMessage();
            });
            window.ethereum.on("chainChanged", async () => {
                const accts = await window.ethereum.request({ method: "eth_accounts" });
                if (accts.length) { await setup(accts); updateTopBar(); if (contract) await refreshMessage(); }
                else resetUI();
            });
        }

        function resetUI() {
            provider = signer = contract = null; account = chainId = null;
            connectBtn.textContent = "🔗 连接 MetaMask"; connectBtn.className = "btn btn-primary";
            publishBtn.disabled = refreshBtn.disabled = true;
            netChip.className = "chip chip-warn"; netLabel.textContent = "未连接";
            addrTag.style.display = "none"; addrRow.style.display = "none";
            msgContent.textContent = "— 暂无留言 —"; msgContent.className = "content empty";
            msgMeta.style.display = "none";
        }

        // ── 页面初始化 ──
        (async () => {
            if (!window.ethereum) {
                connectBtn.textContent = "⚠️ 需要 MetaMask"; connectBtn.disabled = true;
                return;
            }
            try {
                const accts = await window.ethereum.request({ method: "eth_accounts" });
                if (accts.length) {
                    await setup(accts);
                    if (CONTRACT_ADDRESS) { initContract(); await refreshMessage(); }
                }
            } catch (_) {}
        })();
    </script>
</body>
</html>

```

---

## 功能清单

| 功能 | 实现方式 |
|------|----------|
| **部署指南** | 可折叠卡片，5 步图文引导 Remix 部署流程 |
| **连接钱包** | `ethers.BrowserProvider` + `eth_requestAccounts` |
| **读取留言** | 页面加载自动调用 `contract.message()`，也有手动刷新按钮 |
| **写入留言** | 输入框 + 按钮 → `contract.write(text)` → 发送交易 |
| **状态反馈** | Pending（黄色旋转动画）→ 成功（绿色 ✅ 含区块号）→ 失败（红色） |
| **Glassmorphism** | 毛玻璃卡片 + 模糊光晕背景 + Inter 字体 |
| **字符限制** | `maxlength="200"` + 实时字数统计（>180 变黄警告） |
| **账户切换** | `accountsChanged` 监听，自动重连并刷新留言 |
| **链切换** | `chainChanged` 监听，自动更新网络状态 |
| **网络检测** | 非 Monad Testnet显示红色警告，支持一键切换 |
| **错误处理** | 无 MetaMask / 拒绝连接 / 拒绝交易 均有提示 |

---
### 在CodeBuddy CN中的Cloud Studio 部署后的链接（可打开，是在有我的合约地址的前提下，会消耗gas)：(链接已过期)http://fc3ce12862864904a0e926dbe7dcd0b8.codebuddy.cloudstudio.run/

<img width="922" height="983" alt="1444a9fe408c2bb64c2628264208a681" src="https://github.com/user-attachments/assets/d4ce7512-6889-4613-8759-b90ddc1f45c8" />

<img width="1891" height="1037" alt="6aa7b123f9daca417be728ac14a309d1" src="https://github.com/user-attachments/assets/cd141c42-891c-4f2a-bbb1-29e23c07b3f4" />

## 使用步骤

1. 在 Remix 部署合约 → 复制地址
2. 打开 `index.html`，找到顶部 `CONTRACT_ADDRESS = ""`(应该是在243行)，粘贴在Remix部署生成的合约地址后再保存关闭后再打开网址
3. 连接 MetaMask（确保在Monad Testnet测试网）
4. 输入留言 → 发布 → 查看链上结果
