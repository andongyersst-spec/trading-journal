import React, { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { motion } from "framer-motion";
import { LineChart, Line, XAxis, YAxis, Tooltip, PieChart, Pie, Cell, ResponsiveContainer } from "recharts";

export default function TradingJournal() {
  const [trades, setTrades] = useState([]);
  const [profit, setProfit] = useState("");
  const [tradeDate, setTradeDate] = useState("");
  const [startingBalance, setStartingBalance] = useState(1000);
  const [balance, setBalance] = useState(1000);
  const [editingTrade, setEditingTrade] = useState(null);
  const [confirmDeleteId, setConfirmDeleteId] = useState(null);

  // ---- Helpers ----
  const parseNum = (v) => {
    const n = typeof v === "number" ? v : parseFloat(v);
    return isNaN(n) ? 0 : n;
  };

  const recalcBalances = (updatedTrades, base) => {
    const start = base !== undefined ? parseNum(base) : parseNum(startingBalance);
    // Sort by date asc to keep balance timeline correct when backfilling dates
    const sorted = [...updatedTrades].sort((a, b) => new Date(a.date) - new Date(b.date));
    let running = start;
    const withBalances = sorted.map((t) => {
      running += parseNum(t.profit);
      return { ...t, balance: running };
    });
    setTrades(withBalances);
    setBalance(running);
  };

  // ---- Load from localStorage on mount ----
  useEffect(() => {
    try {
      const savedTradesRaw = localStorage.getItem("trades");
      const savedStartRaw = localStorage.getItem("startingBalance");
      const savedStart = savedStartRaw ? parseFloat(savedStartRaw) : 1000;
      const loadedTrades = savedTradesRaw
        ? JSON.parse(savedTradesRaw).map((t) => ({ ...t, date: new Date(t.date) }))
        : [];

      setStartingBalance(isNaN(savedStart) ? 1000 : savedStart);
      recalcBalances(loadedTrades, isNaN(savedStart) ? 1000 : savedStart);
    } catch (e) {
      // if corrupted storage, reset
      setStartingBalance(1000);
      setTrades([]);
      setBalance(1000);
    }
  }, []);

  // ---- Persist to localStorage ----
  useEffect(() => {
    localStorage.setItem("trades", JSON.stringify(trades));
    localStorage.setItem("balance", String(balance));
    localStorage.setItem("startingBalance", String(startingBalance));
  }, [trades, balance, startingBalance]);

  // ---- Actions ----
  const addOrUpdateTrade = () => {
    if (profit === "") return;
    const dateObj = tradeDate ? new Date(tradeDate) : new Date();
    const item = {
      id: editingTrade ? editingTrade.id : Date.now(),
      date: dateObj,
      profit: parseNum(profit),
    };

    let updated;
    if (editingTrade) {
      updated = trades.map((t) => (String(t.id) === String(editingTrade.id) ? { ...t, ...item } : t));
    } else {
      updated = [...trades, item];
    }
    recalcBalances(updated);
    setEditingTrade(null);
    setProfit("");
    setTradeDate("");
  };

  const startEdit = (trade) => {
    setEditingTrade(trade);
    setProfit(String(trade.profit));
    setTradeDate(new Date(trade.date).toISOString().slice(0, 10));
  };

  const requestDelete = (id) => {
    // Show in-app modal; fallback to native confirm if something blocks the modal
    setConfirmDeleteId(id);
  };
  const cancelDelete = () => setConfirmDeleteId(null);
  const confirmDelete = () => {
    const id = confirmDeleteId;
    if (id == null) return;
    const updated = trades.filter((t) => String(t.id) !== String(id));
    setConfirmDeleteId(null);
    recalcBalances(updated);
  };

  // Close modal with ESC or backdrop click
  useEffect(() => {
    const onKey = (e) => {
      if (e.key === "Escape") cancelDelete();
    };
    if (confirmDeleteId != null) window.addEventListener("keydown", onKey);
    return () => window.removeEventListener("keydown", onKey);
  }, [confirmDeleteId]);

  // ---- Stats ----
  const calcWinRate = (data) => {
    if (!data.length) return 0;
    const wins = data.filter((t) => parseNum(t.profit) > 0).length;
    return ((wins / data.length) * 100).toFixed(2);
  };

  const overallWinRate = calcWinRate(trades);

  const thisMonthTrades = trades.filter((t) => {
    const now = new Date();
    const d = new Date(t.date);
    return d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
  });
  const monthlyWinRate = calcWinRate(thisMonthTrades);

  const winLossData = [
    { name: "Wins", value: trades.filter((t) => parseNum(t.profit) > 0).length },
    { name: "Losses", value: trades.filter((t) => parseNum(t.profit) <= 0).length },
  ];

  const COLORS = ["#4ade80", "#f87171"];

  const monthlySummary = trades.reduce((acc, t) => {
    const d = new Date(t.date);
    const monthKey = `${d.getFullYear()}-${d.getMonth() + 1}`;
    if (!acc[monthKey]) acc[monthKey] = { profit: 0, trades: 0, wins: 0 };
    acc[monthKey].profit += parseNum(t.profit);
    acc[monthKey].trades += 1;
    if (parseNum(t.profit) > 0) acc[monthKey].wins += 1;
    return acc;
  }, {});

  const monthlySummaryArray = Object.keys(monthlySummary)
    .sort((a, b) => new Date(a + "-01") - new Date(b + "-01"))
    .map((key) => {
      const [year, month] = key.split("-");
      const tradesCount = monthlySummary[key].trades;
      const wins = monthlySummary[key].wins;
      const winRate = tradesCount ? ((wins / tradesCount) * 100).toFixed(2) : 0;
      return {
        month: `${year}-${String(month).padStart(2, "0")}`,
        profit: monthlySummary[key].profit,
        trades: tradesCount,
        winRate,
      };
    });

  // ---- UI ----
  return (
    <div className="min-h-screen bg-gray-50 p-4 sm:p-6">
      <motion.h1
        className="text-2xl sm:text-3xl font-bold mb-4 sm:mb-6 text-center"
        initial={{ opacity: 0, y: -20 }}
        animate={{ opacity: 1, y: 0 }}
      >
        📈 Personal Trading Journal
      </motion.h1>

      <Card className="mx-auto max-w-screen-lg p-4 sm:p-6 shadow-lg rounded-2xl">
        <CardContent className="p-0">
          {/* Add / Edit form */}
          <div className="flex flex-col sm:flex-row flex-wrap gap-2 sm:gap-3 mb-4">
            <Input
              type="number"
              step="any"
              inputMode="decimal"
              placeholder="Profit / Loss"
              value={profit}
              onChange={(e) => setProfit(e.target.value)}
              className="sm:flex-1 min-w-[140px]"
            />
            <Input
              type="date"
              value={tradeDate}
              onChange={(e) => setTradeDate(e.target.value)}
              className="min-w-[150px]"
            />
            <Button className="w-full sm:w-auto" onClick={addOrUpdateTrade}>
              {editingTrade ? "Update Trade" : "Add Trade"}
            </Button>
          </div>

          {/* Starting balance */}
          <div className="flex flex-col sm:flex-row gap-2 mb-4 items-start sm:items-center">
            <Input
              type="number"
              step="any"
              inputMode="decimal"
              placeholder="Starting Balance"
              value={startingBalance}
              onChange={(e) => {
                const val = parseFloat(e.target.value);
                if (!isNaN(val)) {
                  setStartingBalance(val);
                  recalcBalances(trades, val);
                }
              }}
              className="w-full sm:max-w-xs"
            />
          </div>

          {/* KPIs */}
          <div className="grid grid-cols-1 md:grid-cols-3 gap-3 sm:gap-4 mb-6">
            <div className="bg-white p-3 sm:p-4 rounded-xl shadow">
              <h2 className="text-base sm:text-lg font-semibold">Monthly Win Rate</h2>
              <p className="text-xl sm:text-2xl font-bold text-green-600">{monthlyWinRate}%</p>
            </div>
            <div className="bg-white p-3 sm:p-4 rounded-xl shadow">
              <h2 className="text-base sm:text-lg font-semibold">Overall Win Rate</h2>
              <p className="text-xl sm:text-2xl font-bold text-blue-600">{overallWinRate}%</p>
            </div>
            <div className="bg-white p-3 sm:p-4 rounded-xl shadow">
              <h2 className="text-base sm:text-lg font-semibold">Current Balance</h2>
              <p className="text-xl sm:text-2xl font-bold text-purple-600">${balance}</p>
            </div>
          </div>

          {/* Charts */}
          <div className="grid grid-cols-1 md:grid-cols-2 gap-3 sm:gap-6 mb-6">
            <div className="bg-white p-3 sm:p-4 rounded-xl shadow h-64 sm:h-72">
              <h2 className="text-base sm:text-lg font-semibold mb-2">Balance Over Time</h2>
              <ResponsiveContainer width="100%" height="100%">
                <LineChart
                  data={[{ date: "Start", balance: startingBalance }, ...trades.map((t) => ({ date: new Date(t.date).toLocaleDateString(), balance: t.balance }))]}
                >
                  <XAxis dataKey="date" />
                  <YAxis />
                  <Tooltip />
                  <Line type="monotone" dataKey="balance" stroke="#3b82f6" strokeWidth={3} />
                </LineChart>
              </ResponsiveContainer>
            </div>

            <div className="bg-white p-3 sm:p-4 rounded-xl shadow h-64 sm:h-72">
              <h2 className="text-base sm:text-lg font-semibold mb-2">Win/Loss Distribution</h2>
              <ResponsiveContainer width="100%" height="100%">
                <PieChart>
                  <Pie data={winLossData} dataKey="value" outerRadius={90} label>
                    {winLossData.map((entry, index) => (
                      <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                    ))}
                  </Pie>
                  <Tooltip />
                </PieChart>
              </ResponsiveContainer>
            </div>
          </div>

          {/* Monthly Summary Table */}
          <div className="bg-white p-3 sm:p-4 rounded-xl shadow mb-6 overflow-x-auto">
            <h2 className="text-base sm:text-lg font-semibold mb-2">Monthly P&L Summary</h2>
            <table className="w-full text-left border-collapse text-sm sm:text-base">
              <thead>
                <tr className="border-b">
                  <th className="p-2">Month</th>
                  <th className="p-2">Total Profit/Loss</th>
                  <th className="p-2">Number of Trades</th>
                  <th className="p-2">Win Rate</th>
                </tr>
              </thead>
              <tbody>
                {monthlySummaryArray.map((row, idx) => (
                  <tr key={idx} className="border-b">
                    <td className="p-2">{row.month}</td>
                    <td className={`p-2 font-semibold ${row.profit >= 0 ? "text-green-600" : "text-red-600"}`}>{row.profit}</td>
                    <td className="p-2">{row.trades}</td>
                    <td className="p-2 font-bold">{row.winRate}%</td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>

          {/* Trade History */}
          <h2 className="text-base sm:text-lg font-bold mb-2">Trade History</h2>
          <ul className="space-y-2 max-h-64 overflow-y-auto">
            {trades.map((t) => (
              <li
                key={t.id}
                className={`p-3 sm:p-4 rounded-lg shadow flex flex-col sm:flex-row sm:justify-between sm:items-center gap-2 ${
                  parseNum(t.profit) > 0 ? "bg-green-100" : "bg-red-100"
                }`}
              >
                <div className="flex flex-col">
                  <span className="text-sm sm:text-base">{new Date(t.date).toLocaleDateString()}</span>
                  <span className="font-semibold">{t.profit}</span>
                  <span className="font-bold">Bal: ${t.balance}</span>
                </div>
                <div className="flex gap-2">
                  <Button size="sm" variant="outline" className="w-full sm:w-auto" onClick={() => startEdit(t)}>
                    Edit
                  </Button>
                  <Button
                    size="sm"
                    variant="destructive"
                    className="w-full sm:w-auto"
                    onClick={() => {
                      // open modal; also fallback to native confirm on very old browsers
                      setConfirmDeleteId(t.id);
                    }}
                  >
                    Delete
                  </Button>
                </div>
              </li>
            ))}
          </ul>
        </CardContent>
      </Card>

      {/* In-app Confirm Delete Modal */}
      {confirmDeleteId !== null && (
        <div
          className="fixed inset-0 bg-black/50 flex items-center justify-center z-50"
          onClick={cancelDelete}
        >
          <div
            role="dialog"
            aria-modal="true"
            className="bg-white p-6 rounded-2xl shadow-2xl max-w-sm w-[92%] sm:w-full"
            onClick={(e) => e.stopPropagation()}
          >
            <h3 className="text-lg font-semibold mb-2">Delete this trade?</h3>
            <p className="text-sm text-gray-600 mb-4">This action cannot be undone.</p>
            <div className="flex flex-col sm:flex-row justify-end gap-2">
              <Button variant="outline" className="w-full sm:w-auto" onClick={cancelDelete}>
                Cancel
              </Button>
              <Button variant="destructive" className="w-full sm:w-auto" onClick={confirmDelete}>
                Delete
              </Button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
