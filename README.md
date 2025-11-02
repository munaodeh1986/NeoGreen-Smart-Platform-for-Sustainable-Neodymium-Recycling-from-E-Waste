import React, { useState, useEffect } from 'react';
import { Search, Package, BarChart3, Users, LogOut, Upload, QrCode, Award, MapPin, TrendingUp, Database, Wifi, FileText, Download, Menu, X, Bell, ChevronDown, Filter, Calendar, Eye } from 'lucide-react';

const RecycleIcon = () => (
  <svg className="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
    <path d="M21.82 15.42l-2.5-4.33a1 1 0 00-.87-.5h-.1l-2.7.37 1.64-2.84a1 1 0 00-.37-1.37l-2.6-1.5a1 1 0 00-1.37.37L9.3 10.96l-.97-1.68a1 1 0 00-1.37-.37l-2.6 1.5a1 1 0 00-.37 1.37l2.5 4.33a1 1 0 00.87.5h.1l2.7-.37-1.64 2.84a1 1 0 00.37 1.37l2.6 1.5a1 1 0 001.37-.37l3.65-6.33.97 1.68a1 1 0 001.37.37l2.6-1.5a1 1 0 00.37-1.37z"/>
  </svg>
);

const App = () => {
  const [activeTab, setActiveTab] = useState('dashboard');
  const [devices, setDevices] = useState([]);
  const [users, setUsers] = useState([]);
  const [iotStatus, setIotStatus] = useState({ connected: 12, active: 8 });
  const [rewards, setRewards] = useState([]);
  const [sidebarOpen, setSidebarOpen] = useState(true);
  const [searchQuery, setSearchQuery] = useState('');
  const [filterStatus, setFilterStatus] = useState('all');
  const [notifications] = useState(3);

  useEffect(() => {
    setDevices([
      { id: 'DEV001', type: 'HDD', brand: 'Seagate', model: 'ST3000DM001', status: 'delivered', ndGrams: 1.8, owner: 'Ahmed Khalil', center: 'Riyadh Center', timestamp: '2024-01-15' },
      { id: 'DEV002', type: 'Speaker', brand: 'Sony', model: 'SRS-XB33', status: 'processed', ndGrams: 0.6, owner: 'Sarah Al-Mansoori', center: 'Dubai Center', timestamp: '2024-01-14' },
      { id: 'DEV003', type: 'Motor', brand: 'Panasonic', model: 'MH250', status: 'analyzed', ndGrams: 2.3, owner: 'Mohammed Al-Farsi', center: 'Jeddah Center', timestamp: '2024-01-13' },
      { id: 'DEV004', type: 'Laptop', brand: 'Dell', model: 'XPS 15', status: 'processing', ndGrams: 0.9, owner: 'Fatima Hassan', center: 'Riyadh Center', timestamp: '2024-01-12' },
      { id: 'DEV005', type: 'Phone', brand: 'Samsung', model: 'Galaxy S21', status: 'delivered', ndGrams: 0.3, owner: 'Omar Ali', center: 'Dubai Center', timestamp: '2024-01-11' }
    ]);

    setUsers([
      { id: 'USR001', name: 'Admin User', role: 'admin', email: 'admin@neogreen.com', devices: 0, points: 0 },
      { id: 'USR002', name: 'Ahmed Khalil', role: 'citizen', email: 'ahmed@example.com', devices: 1, points: 180 },
      { id: 'USR003', name: 'Sarah Al-Mansoori', role: 'university', email: 'sarah@university.edu', devices: 1, points: 60 },
      { id: 'USR004', name: 'Mohammed Al-Farsi', role: 'citizen', email: 'mohammed@example.com', devices: 1, points: 230 },
      { id: 'USR005', name: 'Fatima Hassan', role: 'business', email: 'fatima@business.com', devices: 1, points: 90 }
    ]);

    setRewards([
      { userId: 'USR002', points: 180, tokens: 18 },
      { userId: 'USR003', points: 60, tokens: 6 },
      { userId: 'USR004', points: 230, tokens: 23 },
      { userId: 'USR005', points: 90, tokens: 9 }
    ]);
  }, []);

  const stats = {
    totalDevices: devices.length,
    totalNdGrams: devices.reduce((sum, device) => sum + device.ndGrams, 0).toFixed(2),
    activeUsers: users.length,
    co2Saved: (devices.length * 0.5).toFixed(1)
  };

  const tabs = [
    { id: 'dashboard', label: 'Dashboard', icon: BarChart3 },
    { id: 'devices', label: 'Devices', icon: Package },
    { id: 'users', label: 'Users', icon: Users },
    { id: 'iot', label: 'IoT Integration', icon: Wifi },
    { id: 'rewards', label: 'Rewards', icon: Award },
    { id: 'reports', label: 'Reports', icon: FileText }
  ];

  const filteredDevices = devices.filter(device => {
    const matchesSearch = device.type.toLowerCase().includes(searchQuery.toLowerCase()) ||
                         device.brand.toLowerCase().includes(searchQuery.toLowerCase()) ||
                         device.owner.toLowerCase().includes(searchQuery.toLowerCase());
    const matchesFilter = filterStatus === 'all' || device.status === filterStatus;
    return matchesSearch && matchesFilter;
  });

  const DeviceCard = ({ device }) => (
    <div className="bg-white rounded-xl shadow-sm hover:shadow-xl transition-all duration-300 overflow-hidden border border-gray-100 transform hover:-translate-y-1">
      <div className="h-2 bg-gradient-to-r from-blue-500 to-green-500"></div>
      <div className="p-5">
        <div className="flex justify-between items-start mb-4">
          <div className="flex items-start space-x-3">
            <div className="w-12 h-12 bg-gradient-to-br from-blue-50 to-blue-100 rounded-lg flex items-center justify-center">
              <Package className="w-6 h-6 text-blue-600" />
            </div>
            <div>
              <h3 className="font-semibold text-gray-900 text-lg">{device.type}</h3>
              <p className="text-sm text-gray-600">{device.brand} {device.model}</p>
            </div>
          </div>
          <span className={`px-3 py-1 rounded-full text-xs font-semibold ${
            device.status === 'delivered' ? 'bg-blue-100 text-blue-700' :
            device.status === 'processed' ? 'bg-green-100 text-green-700' :
            device.status === 'processing' ? 'bg-yellow-100 text-yellow-700' :
            'bg-purple-100 text-purple-700'
          }`}>
            {device.status}
          </span>
        </div>
        
        <div className="space-y-3">
          <div className="flex items-center justify-between p-2 bg-gray-50 rounded-lg">
            <span className="text-sm text-gray-600 flex items-center">
              <Database className="w-4 h-4 mr-2 text-green-600" />
              Neodymium
            </span>
            <span className="font-bold text-green-600">{device.ndGrams}g</span>
          </div>
          
          <div className="flex items-center justify-between p-2 bg-gray-50 rounded-lg">
            <span className="text-sm text-gray-600 flex items-center">
              <Users className="w-4 h-4 mr-2 text-blue-600" />
              Owner
            </span>
            <span className="font-medium text-gray-900">{device.owner}</span>
          </div>
          
          <div className="flex items-center justify-between p-2 bg-gray-50 rounded-lg">
            <span className="text-sm text-gray-600 flex items-center">
              <MapPin className="w-4 h-4 mr-2 text-red-600" />
              Center
            </span>
            <span className="font-medium text-gray-900">{device.center}</span>
          </div>
          
          <div className="flex items-center justify-between p-2 bg-gray-50 rounded-lg">
            <span className="text-sm text-gray-600 flex items-center">
              <Calendar className="w-4 h-4 mr-2 text-purple-600" />
              Date
            </span>
            <span className="font-medium text-gray-900">{device.timestamp}</span>
          </div>
        </div>
        
        <button className="mt-4 w-full bg-gradient-to-r from-blue-600 to-blue-700 text-white py-2 px-4 rounded-lg hover:from-blue-700 hover:to-blue-800 transition-all duration-200 flex items-center justify-center space-x-2">
          <Eye className="w-4 h-4" />
          <span>View Details</span>
        </button>
      </div>
    </div>
  );

  const StatCard = ({ title, value, icon: Icon, gradient }) => (
    <div className={`bg-gradient-to-br ${gradient} rounded-2xl p-6 text-white shadow-lg hover:shadow-2xl transition-all duration-300 transform hover:scale-105`}>
      <div className="flex items-center justify-between">
        <div>
          <p className="text-white opacity-80 text-sm font-medium mb-2">{title}</p>
          <p className="text-4xl font-bold">{value}</p>
          <div className="mt-2 flex items-center space-x-1">
            <TrendingUp className="w-4 h-4" />
            <span className="text-sm">+12% this month</span>
          </div>
        </div>
        <div className="w-16 h-16 bg-white bg-opacity-20 rounded-2xl flex items-center justify-center backdrop-blur-sm">
          <Icon className="w-8 h-8" />
        </div>
      </div>
    </div>
  );

  const renderContent = () => {
    switch (activeTab) {
      case 'dashboard':
        return (
          <div className="space-y-8 animate-fadeIn">
            <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
              <StatCard 
                title="Total Devices" 
                value={stats.totalDevices} 
                icon={Package} 
                gradient="from-blue-500 via-blue-600 to-blue-700"
              />
              <StatCard 
                title="Neodymium (g)" 
                value={stats.totalNdGrams} 
                icon={Database} 
                gradient="from-green-500 via-green-600 to-green-700"
              />
              <StatCard 
                title="Active Users" 
                value={stats.activeUsers} 
                icon={Users} 
                gradient="from-purple-500 via-purple-600 to-purple-700"
              />
              <StatCard 
                title="CO₂ Saved (kg)" 
                value={stats.co2Saved} 
                icon={TrendingUp} 
                gradient="from-orange-500 via-orange-600 to-orange-700"
              />
            </div>
            
            <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
              <div className="lg:col-span-2 bg-white rounded-2xl shadow-lg p-6">
                <div className="flex items-center justify-between mb-6">
                  <h3 className="text-xl font-bold text-gray-900">Recent Devices</h3>
                  <button className="text-blue-600 hover:text-blue-700 font-medium text-sm flex items-center">
                    View All
                  </button>
                </div>
                <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                  {devices.slice(0, 4).map(device => (
                    <DeviceCard key={device.id} device={device} />
                  ))}
                </div>
              </div>
              
              <div className="space-y-6">
                <div className="bg-gradient-to-br from-blue-500 to-purple-600 rounded-2xl shadow-lg p-6 text-white">
                  <h3 className="text-lg font-semibold mb-4 flex items-center">
                    <Wifi className="w-5 h-5 mr-2" />
                    IoT Status
                  </h3>
                  <div className="space-y-4">
                    <div className="flex items-center justify-between bg-white bg-opacity-20 backdrop-blur-sm rounded-lg p-3">
                      <div className="flex items-center space-x-3">
                        <div className="w-3 h-3 bg-green-400 rounded-full animate-pulse"></div>
                        <span>Connected Devices</span>
                      </div>
                      <span className="font-bold text-xl">{iotStatus.connected}</span>
                    </div>
                    <div className="flex items-center justify-between bg-white bg-opacity-20 backdrop-blur-sm rounded-lg p-3">
                      <div className="flex items-center space-x-3">
                        <div className="w-3 h-3 bg-blue-400 rounded-full animate-pulse"></div>
                        <span>Active Processes</span>
                      </div>
                      <span className="font-bold text-xl">{iotStatus.active}</span>
                    </div>
                  </div>
                </div>
                
                <div className="bg-white rounded-2xl shadow-lg p-6">
                  <h3 className="text-lg font-bold text-gray-900 mb-4 flex items-center">
                    <Award className="w-5 h-5 mr-2 text-yellow-500" />
                    Top Contributors
                  </h3>
                  <div className="space-y-3">
                    {rewards.sort((a, b) => b.points - a.points).slice(0, 3).map((reward, index) => {
                      const user = users.find(u => u.id === reward.userId);
                      return (
                        <div key={index} className="flex items-center justify-between p-3 bg-gradient-to-r from-yellow-50 to-orange-50 rounded-lg">
                          <div className="flex items-center space-x-3">
                            <div className={`w-8 h-8 rounded-full flex items-center justify-center font-bold text-white ${
                              index === 0 ? 'bg-yellow-500' : index === 1 ? 'bg-gray-400' : 'bg-orange-400'
                            }`}>
                              {index + 1}
                            </div>
                            <div>
                              <p className="font-medium text-gray-900">{user?.name}</p>
                              <p className="text-xs text-gray-600">{reward.points} points</p>
                            </div>
                          </div>
                          <Award className="w-5 h-5 text-yellow-500" />
                        </div>
                      );
                    })}
                  </div>
                </div>
              </div>
            </div>
          </div>
        );
      
      case 'devices':
        return (
          <div className="space-y-6 animate-fadeIn">
            <div className="flex flex-col md:flex-row md:items-center justify-between gap-4">
              <h2 className="text-3xl font-bold text-gray-900">Device Management</h2>
              <div className="flex flex-wrap gap-3">
                <button className="flex items-center space-x-2 bg-gradient-to-r from-blue-600 to-blue-700 text-white px-5 py-2.5 rounded-xl hover:from-blue-700 hover:to-blue-800 transition-all duration-200 shadow-lg">
                  <Upload className="w-4 h-4" />
                  <span>Register Device</span>
                </button>
                <button className="flex items-center space-x-2 bg-white text-gray-700 px-5 py-2.5 rounded-xl hover:bg-gray-50 transition-all duration-200 shadow-lg border border-gray-200">
                  <QrCode className="w-4 h-4" />
                  <span>Scan QR</span>
                </button>
              </div>
            </div>
            
            <div className="bg-white rounded-2xl shadow-lg p-6">
              <div className="flex flex-col md:flex-row gap-4 mb-6">
                <div className="flex-1 relative">
                  <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
                  <input
                    type="text"
                    placeholder="Search devices..."
                    value={searchQuery}
                    onChange={(e) => setSearchQuery(e.target.value)}
                    className="w-full pl-10 pr-4 py-3 border border-gray-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                  />
                </div>
                <div className="relative">
                  <Filter className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
                  <select
                    value={filterStatus}
                    onChange={(e) => setFilterStatus(e.target.value)}
                    className="pl-10 pr-8 py-3 border border-gray-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent appearance-none bg-white"
                  >
                    <option value="all">All Status</option>
                    <option value="delivered">Delivered</option>
                    <option value="processed">Processed</option>
                    <option value="processing">Processing</option>
                    <option value="analyzed">Analyzed</option>
                  </select>
                </div>
              </div>
              
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                {filteredDevices.map(device => (
                  <DeviceCard key={device.id} device={device} />
                ))}
              </div>
            </div>
          </div>
        );
      
      case 'users':
        return (
          <div className="space-y-6 animate-fadeIn">
            <h2 className="text-3xl font-bold text-gray-900">User Management</h2>
            <div className="bg-white rounded-2xl shadow-lg overflow-hidden">
              <div className="overflow-x-auto">
                <table className="min-w-full divide-y divide-gray-200">
                  <thead className="bg-gradient-to-r from-gray-50 to-gray-100">
                    <tr>
                      <th className="px-6 py-4 text-left text-xs font-bold text-gray-600 uppercase tracking-wider">User</th>
                      <th className="px-6 py-4 text-left text-xs font-bold text-gray-600 uppercase tracking-wider">Role</th>
                      <th className="px-6 py-4 text-left text-xs font-bold text-gray-600 uppercase tracking-wider">Devices</th>
                      <th className="px-6 py-4 text-left text-xs font-bold text-gray-600 uppercase tracking-wider">Points</th>
                      <th className="px-6 py-4 text-left text-xs font-bold text-gray-600 uppercase tracking-wider">Actions</th>
                    </tr>
                  </thead>
                  <tbody className="bg-white divide-y divide-gray-200">
                    {users.map(user => (
                      <tr key={user.id} className="hover:bg-blue-50 transition-colors">
                        <td className="px-6 py-4 whitespace-nowrap">
                          <div className="flex items-center">
                            <div className="w-10 h-10 bg-gradient-to-br from-blue-500 to-purple-600 rounded-full flex items-center justify-center text-white font-bold">
                              {user.name.charAt(0)}
                            </div>
                            <div className="ml-4">
                              <div className="font-medium text-gray-900">{user.name}</div>
                              <div className="text-sm text-gray-500">{user.email}</div>
                            </div>
                          </div>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap">
                          <span className={`px-3 py-1 rounded-full text-xs font-semibold ${
                            user.role === 'admin' ? 'bg-red-100 text-red-700' :
                            user.role === 'university' ? 'bg-purple-100 text-purple-700' :
                            user.role === 'business' ? 'bg-green-100 text-green-700' :
                            'bg-blue-100 text-blue-700'
                          }`}>
                            {user.role}
                          </span>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap">
                          <div className="flex items-center">
                            <Package className="w-4 h-4 mr-2 text-gray-400" />
                            <span className="font-medium">{user.devices}</span>
                          </div>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap">
                          <div className="flex items-center">
                            <Award className="w-4 h-4 mr-2 text-yellow-500" />
                            <span className="font-bold text-green-600">{user.points}</span>
                          </div>
                        </td>
                        <td className="px-6 py-4 whitespace-nowrap text-sm font-medium">
                          <button className="text-blue-600 hover:text-blue-900 mr-4 font-semibold">Edit</button>
                          <button className="text-red-600 hover:text-red-900 font-semibold">Delete</button>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        );
      
      case 'iot':
        return (
          <div className="space-y-6 animate-fadeIn">
            <h2 className="text-3xl font-bold text-gray-900">IoT Integration</h2>
            <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
              <div className="bg-white rounded-2xl shadow-lg p-6">
                <h3 className="text-xl font-semibold mb-4 flex items-center">
                  <Wifi className="w-5 h-5 mr-2 text-blue-600" />
                  MQTT Connection
                </h3>
                <div className="space-y-4">
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-2">Broker Address</label>
                    <input 
                      type="text" 
                      defaultValue="mqtt://localhost:1883"
                      className="w-full px-4 py-3 border border-gray-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    />
                  </div>
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-2">Topic</label>
                    <input 
                      type="text" 
                      defaultValue="neogreen/devices/+"
                      className="w-full px-4 py-3 border border-gray-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    />
                  </div>
                  <button className="w-full bg-gradient-to-r from-green-600 to-green-700 text-white py-3 px-4 rounded-xl hover:from-green-700 hover:to-green-800 transition-all duration-200 shadow-lg flex items-center justify-center space-x-2">
                    <Wifi className="w-5 h-5" />
                    <span>Connect to MQTT</span>
                  </button>
                </div>
              </div>
              
              <div className="bg-gradient-to-br from-blue-500 to-purple-600 rounded-2xl shadow-lg p-6 text-white">
                <h3 className="text-xl font-semibold mb-4">Arduino Integration</h3>
                <div className="space-y-4">
                  <div className="bg-black bg-opacity-30 backdrop-blur-sm p-4 rounded-xl font-mono text-sm overflow-x-auto">
                    <code className="text-green-300 whitespace-pre">
{`// Arduino MQTT Example
#include <PubSubClient.h>

const char* mqtt_server = 
  "localhost";

void setup() {
  // Initialize sensors
  // Connect to MQTT
}

void loop() {
  client.publish(
    "neogreen/devices",
    "data"
  );
}`}
                    </code>
                  </div>
                  <button className="w-full bg-white text-blue-600 py-3 px-4 rounded-xl hover:bg-blue-50 transition-all duration-200 shadow-lg flex items-center justify-center space-x-2 font-semibold">
                    <Download className="w-5 h-5" />
                    <span>Download Arduino Code</span>
                  </button>
                </div>
              </div>
            </div>
            
            <div className="bg-white rounded-2xl shadow-lg p-6">
              <h3 className="text-xl font-semibold mb-4 flex items-center">
                <Database className="w-5 h-5 mr-2 text-green-600" />
                Recent IoT Messages
              </h3>
              <div className="space-y-3">
                {[
                  { id: 'MSG001', device: 'DEV001', sensor: 'hall', value: '0.85', timestamp: '2024-01-15 14:30:22' },
                  { id: 'MSG002', device: 'DEV002', sensor: 'temperature', value: '25.3', timestamp: '2024-01-15 14:28:15' },
                  { id: 'MSG003', device: 'DEV003', sensor: 'hall', value: '0.92', timestamp: '2024-01-15 14:25:47' }
                ].map(msg => (
                  <div key={msg.id} className="flex justify-between items-center p-4 bg-gradient-to-r from-blue-50 to-purple-50 rounded-xl hover:shadow-md transition-shadow">
                    <div className="flex items-center space-x-3">
                      <div className="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                      <span className="font-semibold text-gray-900">{msg.device}</span>
                      <span className="text-gray-600">-</span>
                      <span className="text-gray-700">{msg.sensor}: <span className="font-bold text-blue-600">{msg.value}</span></span>
                    </div>
                    <span className="text-sm text-gray-500">{msg.timestamp}</span>
                  </div>
                ))}
              </div>
            </div>
          </div>
        );
      
      case 'rewards':
        return (
          <div className="space-y-6 animate-fadeIn">
            <h2 className="text-3xl font-bold text-gray-900">Rewards Program</h2>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div className="bg-white rounded-2xl shadow-lg p-6">
                <h3 className="text-xl font-semibold mb-4 flex items-center">
                  <Award className="w-5 h-5 mr-2 text-yellow-500" />
                  User Rewards
                </h3>
                <div className="space-y-4">
                  {rewards.sort((a, b) => b.points - a.points).map((reward, index) => {
                    const user = users.find(u => u.id === reward.userId);
                    return (
                      <div key={index} className="p-4 bg-gradient-to-r from-yellow-50 via-orange-50 to-red-50 rounded-xl hover:shadow-md transition-all border border-orange-100">
                        <div className="flex justify-between items-center">
                          <div className="flex items-center space-x-3">
                            <div className="w-12 h-12 bg-gradient-to-br from-yellow-400 to-orange-500 rounded-full flex items-center justify-center text-white font-bold text-lg">
                              {user?.name.charAt(0)}
                            </div>
                            <div>
                              <p className="font-semibold text-gray-900">{user?.name}</p>
                              <p className="text-sm text-gray-600">{user?.email}</p>
                            </div>
                          </div>
                          <div className="text-right">
                            <p className="font-bold text-2xl text-blue-600">{reward.points}</p>
                            <p className="text-sm text-gray-600">{reward.tokens} tokens</p>
                          </div>
                        </div>
                      </div>
                    );
                  })}
                </div>
              </div>
              
              <div className="bg-gradient-to-br from-purple-500 to-pink-600 rounded-2xl shadow-lg p-6 text-white">
                <h3 className="text-xl font-semibold mb-4">Reward Settings</h3>
                <div className="space-y-4">
                  <div>
                    <label className="block text-sm font-medium mb-2 opacity-90">Points per gram of Nd</label>
                    <input 
                      type="number" 
                      defaultValue="10"
                      className="w-full px-4 py-3 bg-white bg-opacity-20 backdrop-blur-sm border border-white border-opacity-30 rounded-xl focus:outline-none focus:ring-2 focus:ring-white text-white placeholder-white"
                    />
                  </div>
                  <div>
                    <label className="block text-sm font-medium mb-2 opacity-90">Minimum payout threshold</label>
                    <input 
                      type="number" 
                      defaultValue="100"
                      className="w-full px-4 py-3 bg-white bg-opacity-20 backdrop-blur-sm border border-white border-opacity-30 rounded-xl focus:outline-none focus:ring-2 focus:ring-white text-white placeholder-white"
                    />
                  </div>
                  <button className="w-full bg-white text-purple-600 py-3 px-4 rounded-xl hover:bg-purple-50 transition-all duration-200 shadow-lg font-semibold flex items-center justify-center space-x-2">
                    <Database className="w-5 h-5" />
                    <span>Update Settings</span>
                  </button>
                </div>
              </div>
            </div>
            
            <div className="bg-white rounded-2xl shadow-lg p-6">
              <h3 className="text-xl font-semibold mb-6">Rewards Leaderboard</h3>
              <div className="space-y-3">
                {rewards.sort((a, b) => b.points - a.points).map((reward, index) => {
                  const user = users.find(u => u.id === reward.userId);
                  return (
                    <div key={index} className="flex items-center justify-between p-4 bg-gradient-to-r from-gray-50 to-blue-50 rounded-xl hover:shadow-md transition-all">
                      <div className="flex items-center space-x-4">
                        <div className={`w-12 h-12 rounded-full flex items-center justify-center font-bold text-white text-lg ${
                          index === 0 ? 'bg-gradient-to-br from-yellow-400 to-yellow-600' :
                          index === 1 ? 'bg-gradient-to-br from-gray-300 to-gray-500' :
                          index === 2 ? 'bg-gradient-to-br from-orange-400 to-orange-600' :
                          'bg-gradient-to-br from-blue-400 to-blue-600'
                        }`}>
                          {index + 1}
                        </div>
                        <div>
                          <p className="font-semibold text-gray-900">{user?.name}</p>
                          <p className="text-sm text-gray-600">{user?.role}</p>
                        </div>
                      </div>
                      <div className="flex items-center space-x-6">
                        <div className="text-right">
                          <p className="font-bold text-2xl text-blue-600">{reward.points}</p>
                          <p className="text-sm text-gray-600">points</p>
                        </div>
                        <div className="text-right">
                          <p className="font-bold text-xl text-green-600">{reward.tokens}</p>
                          <p className="text-sm text-gray-600">tokens</p>
                        </div>
                      </div>
                    </div>
                  );
                })}
              </div>
            </div>
          </div>
        );
      
      case 'reports':
        return (
          <div className="space-y-6 animate-fadeIn">
            <div className="flex flex-col md:flex-row md:items-center justify-between gap-4">
              <h2 className="text-3xl font-bold text-gray-900">Reports & Analytics</h2>
              <div className="flex flex-wrap gap-3">
                <button className="flex items-center space-x-2 bg-gradient-to-r from-green-600 to-green-700 text-white px-5 py-2.5 rounded-xl hover:from-green-700 hover:to-green-800 transition-all duration-200 shadow-lg">
                  <Download className="w-4 h-4" />
                  <span>Export CSV</span>
                </button>
                <button className="flex items-center space-x-2 bg-gradient-to-r from-red-600 to-red-700 text-white px-5 py-2.5 rounded-xl hover:from-red-700 hover:to-red-800 transition-all duration-200 shadow-lg">
                  <Download className="w-4 h-4" />
                  <span>Export PDF</span>
                </button>
              </div>
            </div>
            
            <div className="bg-white rounded-2xl shadow-lg p-6">
              <h3 className="text-xl font-semibold mb-6 flex items-center">
                <Calendar className="w-5 h-5 mr-2 text-blue-600" />
                Monthly Summary - January 2024
              </h3>
              <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div className="text-center p-6 bg-gradient-to-br from-green-50 to-green-100 rounded-xl hover:shadow-lg transition-all">
                  <div className="w-16 h-16 bg-gradient-to-br from-green-500 to-green-600 rounded-2xl flex items-center justify-center mx-auto mb-4">
                    <BarChart3 className="w-8 h-8 text-white" />
                  </div>
                  <p className="text-4xl font-bold text-green-800 mb-2">15</p>
                  <p className="text-gray-700 font-medium">Total Devices</p>
                </div>
                <div className="text-center p-6 bg-gradient-to-br from-blue-50 to-blue-100 rounded-xl hover:shadow-lg transition-all">
                  <div className="w-16 h-16 bg-gradient-to-br from-blue-500 to-blue-600 rounded-2xl flex items-center justify-center mx-auto mb-4">
                    <Database className="w-8 h-8 text-white" />
                  </div>
                  <p className="text-4xl font-bold text-blue-800 mb-2">24.7g</p>
                  <p className="text-gray-700 font-medium">Neodymium</p>
                </div>
                <div className="text-center p-6 bg-gradient-to-br from-orange-50 to-orange-100 rounded-xl hover:shadow-lg transition-all">
                  <div className="w-16 h-16 bg-gradient-to-br from-orange-500 to-orange-600 rounded-2xl flex items-center justify-center mx-auto mb-4">
                    <TrendingUp className="w-8 h-8 text-white" />
                  </div>
                  <p className="text-4xl font-bold text-orange-800 mb-2">7.5kg</p>
                  <p className="text-gray-700 font-medium">CO₂ Saved</p>
                </div>
              </div>
            </div>
            
            <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
              <div className="bg-white rounded-2xl shadow-lg p-6">
                <h3 className="text-xl font-semibold mb-4">Device Type Distribution</h3>
                <div className="h-64 flex items-center justify-center bg-gradient-to-br from-blue-50 to-purple-50 rounded-xl">
                  <div className="text-center">
                    <BarChart3 className="w-16 h-16 text-blue-500 mx-auto mb-3" />
                    <p className="text-gray-600">Chart visualization would appear here</p>
                  </div>
                </div>
              </div>
              
              <div className="bg-white rounded-2xl shadow-lg p-6">
                <h3 className="text-xl font-semibold mb-4">Monthly Trends</h3>
                <div className="h-64 flex items-center justify-center bg-gradient-to-br from-green-50 to-yellow-50 rounded-xl">
                  <div className="text-center">
                    <TrendingUp className="w-16 h-16 text-green-500 mx-auto mb-3" />
                    <p className="text-gray-600">Trend analysis would appear here</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        );
      
      default:
        return null;
    }
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-50 via-blue-50 to-purple-50">
      <style>{`
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(10px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .animate-fadeIn {
          animation: fadeIn 0.5s ease-out;
        }
      `}</style>
      
      <div className="flex">
        <div className={`${sidebarOpen ? 'w-64' : 'w-20'} bg-white shadow-2xl min-h-screen transition-all duration-300 fixed lg:relative z-50`}>
          <div className="p-6 border-b border-gray-200">
            <div className="flex items-center justify-between">
              <div className={`flex items-center space-x-3 ${!sidebarOpen && 'justify-center'}`}>
                <div className="w-10 h-10 bg-gradient-to-br from-green-500 to-green-600 rounded-xl flex items-center justify-center shadow-lg">
                  <RecycleIcon />
                </div>
                {sidebarOpen && (
                  <div>
                    <h1 className="text-xl font-bold bg-gradient-to-r from-green-600 to-blue-600 bg-clip-text text-transparent">NeoGreen</h1>
                    <p className="text-xs text-gray-600">E-Waste Platform</p>
                  </div>
                )}
              </div>
              <button 
                onClick={() => setSidebarOpen(!sidebarOpen)}
                className="lg:hidden p-2 hover:bg-gray-100 rounded-lg"
              >
                {sidebarOpen ? <X className="w-5 h-5" /> : <Menu className="w-5 h-5" />}
              </button>
            </div>
          </div>
          
          <nav className="p-4 space-y-2">
            {tabs.map(tab => {
              const Icon = tab.icon;
              return (
                <button
                  key={tab.id}
                  onClick={() => setActiveTab(tab.id)}
                  className={`w-full flex items-center space-x-3 px-4 py-3 rounded-xl text-left transition-all duration-200 ${
                    activeTab === tab.id 
                      ? 'bg-gradient-to-r from-blue-500 to-blue-600 text-white shadow-lg transform scale-105' 
                      : 'text-gray-700 hover:bg-gray-100'
                  } ${!sidebarOpen && 'justify-center'}`}
                >
                  <Icon className="w-5 h-5" />
                  {sidebarOpen && <span className="font-medium">{tab.label}</span>}
                </button>
              );
            })}
          </nav>
          
          {sidebarOpen && (
            <div className="absolute bottom-0 w-64 p-4 border-t border-gray-200 bg-white">
              <div className="flex items-center justify-between">
                <div className="flex items-center space-x-3">
                  <div className="w-10 h-10 bg-gradient-to-br from-blue-500 to-purple-600 rounded-full flex items-center justify-center shadow-lg">
                    <span className="text-white font-bold text-sm">A</span>
                  </div>
                  <div>
                    <p className="font-semibold text-gray-900 text-sm">Admin User</p>
                    <p className="text-xs text-gray-600">admin@neogreen.com</p>
                  </div>
                </div>
                <button className="p-2 hover:bg-red-50 rounded-lg transition-colors">
                  <LogOut className="w-5 h-5 text-gray-500 hover:text-red-500" />
                </button>
              </div>
            </div>
          )}
        </div>
        
        <div className="flex-1 lg:ml-0">
          <div className="bg-white shadow-md sticky top-0 z-40">
            <div className="px-8 py-4 flex items-center justify-between">
              <button 
                onClick={() => setSidebarOpen(!sidebarOpen)}
                className="lg:hidden p-2 hover:bg-gray-100 rounded-lg"
              >
                <Menu className="w-6 h-6" />
              </button>
              
              <div className="flex-1 max-w-xl mx-auto hidden md:block">
                <div className="relative">
                  <Search className="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
                  <input
                    type="text"
                    placeholder="Search anything..."
                    className="w-full pl-12 pr-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 focus:bg-white transition-all"
                  />
                </div>
              </div>
              
              <div className="flex items-center space-x-4">
                <button className="relative p-2 hover:bg-gray-100 rounded-xl transition-colors">
                  <Bell className="w-6 h-6 text-gray-600" />
                  {notifications > 0 && (
                    <span className="absolute top-0 right-0 w-5 h-5 bg-red-500 text-white text-xs font-bold rounded-full flex items-center justify-center">
                      {notifications}
                    </span>
                  )}
                </button>
              </div>
            </div>
          </div>
          
          <div className="p-8">
            <div className="max-w-7xl mx-auto">
              {renderContent()}
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};

export default App;
